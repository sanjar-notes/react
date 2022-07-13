# 157. useCallback and its dependencies
Created Monday 11 July 2022

### Why
What is the use of the dependency array in `useCallback` ? To answer this, let's think of how `useCallback` works. Consider the following code:
```jsx
import { useState, useCallback } from 'react';

function Main() {
	const [show, setShow] = useState(false);
	const [allowToggle, setAllowToggle] = useState(false);

	const toggleHandler = useCallback(() => {
			if(allowToggle)
				setShow(prev => !prev);
		, []); // Will this handler work?
		
	const allowToggleHandler = () => setAllowToggle(prev => !prev);
		
	return (<>
			{show && 'Message visible'}
			<Button handler={allowToggleHandler}>{allowToggle ? 'Disallow' : 'Allow'}Toggle</Button>
				<Button handler={toggleHandler}>Toggle</Button>		
			</>);
}
```
Will the handler maintain referential integrity between re-evaluations? No, it will not. Reason: `useCallback` *saves* the snapshot of the callback along with all it's variables (even external ones). This means the callback's dependent variable (`allowToggle` in this case) is actually a copy instead of the actual variable reference. Even if the component updates and `allowToggle` becomes `true`, the callback doesn't change.

- In short, the dependency array allows the re-creation of the callback, if it's dependent on external variables. This is *very* important and show be kept in mind.

### How
To make this example work, add `allowToggle` to the dependency array, like so:
```jsx
const toggleHandler = useCallback(() => {
	if(allowToggle)
		setShow(prev => !prev);
}, [allowToggle]); // will work now
```