# 3. Working with multiple states
Created Saturday 24 January 2022

## Why
A component may have more than one state. There are two ways to handle automatic re-rendering. Either use multiple `useState` or create a single object of all state variables (so just one `useState` is needed).

## How
If multiple states are handled individually, then it's simple. But if all state variables are packed into a single state, then care must be taken to also safely retain the un-updated variable in each `setStateMethod` (of `useState`) call.

This must be done because just setting one attribute will **replace** other attributes. A shorthand is to use the **spread operator**, which results in cleaner code.

Note: Spread operator actually merges the attribute, just remember keep the spread operator as the first attribute.

Here's a code example for multiple state:
1. Individual states
```jsx
import React, { useState } from 'React';

function MyComponent () {
	const [count, setCount] = useState(0);
	const [reverseCount, setReverseCount] = useState(999);

	const countClick = () => { setCount(count + 1); };
	const reverseCountClick = () => { setReverseCount(reverseCount - 1); };

	return (
		<div>
			<button onClick={countClick}>+: {count}</button> &nbsp;
			<button onClick={reverseCountClick}>-: {reverseCount} </button>
		</div>
	);
}

export default MultiStateMulti;
```

2. Single state object - all attributes have to be specified during update, otherwise they'll be lost. So we use the spread operator (`...state`) which merges the previous state with the attribute we are updating.
```jsx
import React, { useState } from "react";

function MultiStateSingle() {
	const [state, setState] = useState({ count: 0, reverseCount: 999 });

	const countClick = () => {
		setState({
			...state,
		    count: state.count + 1, // will update/merge existing
		});
	};
	const reverseCountClick = () => {
		setState({
		    ...state,
			reverseCount: state.reverseCount - 1,
		});
	};

	return (
		<div>
			<button onClick={countClick}>+: {state.count}</button> 
			&nbsp;
			<button onClick={reverseCountClick}>-: {state.reverseCount}</button>
		</div>
	);
}

export default MultiStateSingle;
```

## callback instead of value in state update call
There's a BIG catch here. Most of the time, we are updating state based on its current value. This becomes a problem if we are using the spread operator. It is a problem because React actually schedules changes, instead of carrying them out immediately.

To avoid this, pass a function to the updater function instead of a value. This function must have one parameter (which will be the latest state) and return the updated state. The method gets called by the updater, automatically.

The updater code would look like this, ensuring that the latest state is update every-time.
```jsx
const countClick = () => {
	setState( (latestState) => {
		return {
			...latestState,
			count: latestState.count + 1,
		};
	});
};

const reverseCountClick = () => {
	setState( (latestState) => {
		return {
			...latestState,
			reverseCount: latestState.reverseCount - 1,
		};
	});
};

return <></>;
```

Note: FIXME, I've not completely understood why this function instead of direct update is needed, because even if changes are scheduled and not done immediately, the schedule can save a reference to the object, which will ensure latest state at all times.