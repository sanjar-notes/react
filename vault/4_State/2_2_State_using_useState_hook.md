# 2. State using useState hook
Created Saturday 24 January 2022

## Why
This is an implementation of state, so that components are redrawn when state is mutated explicitly. Note that state remains detached from the component lifecycle.

## How
A life-cycle method (informally called a hook) is used. It is added to the component's code.

A variable is captured as state and managed by the hook.
When an update call using the hook is made, the component is re-rendered. So UI is synced with the state.

## What
Here's the syntax:
1. Import `useState` from `react`.
2. Capture a variable using `useState`, and also get back an updater function. Add this code in the component.
3. Update the state using the updater method.
Example
```JSX
import React, { useState } from 'react';

function MyComponent (props) {
	const [title, setTitle] = useState(props.title);

	// some code/event that fires setTitle
	const clickHandler = () => {
		setTitle("Updated!"); // this sets the states and fires a re-render
	}

	return (<div>
			...
			<button onClick = {clickHandler}> Click me </button>
			...
			</div>);
}
```
Also see [project commit](https://github.com/exemplar-codes/expense-tracker-react/commit/45d42efca9e80754120da43d5989c05519a2965f).

## General flow of `useState`
For the skeleton:
```JSX
function MyComponent {
	const [readVar, setVariable] = useState(capture_variable);
	// some code that calls setVariable
	// component code (JSX) returned.
}
```
is:
1. In the first pass:
	1. useState is initialized, state is set internally.
	2. Read variable set to state.
	3. Component is drawn.
2. In the second pass:
	1. useState argument (initialization) is ignored.
	2. State set to setState argument - setState is called from event/timer etc.
	3. Read variable set to state.
	4. Component is drawn.
3.  Step 2 repeats.
Note: `const` is OK for the read variable, because we never assign (`=`) anything to it. It's changed internally.

## Computation of initial state
If the initial state is a large computation, we would not want to include it in the component non-markup code, because it would execute on every re-render. The workaround is to pass a function to `useState` instead of a value (variable). This function will only be run once (when the component first renders), and never again. This way the "initial state" computation is done only once.
