# 117. useReducer hook
Created Tuesday 12 March 2022
- [ ] in vault
    
### Why (when to use it instead of `useState`)
`useReducer` is a syntax sugar for `useState` . It is preferred over `useState` if the state:
- Is complex (has many parts).
- The state and data inside it are highly related (OK, but Why?).
- Types of updates are more, as using `useState` would result in a lot of functions, which makes the JSX or JS code bulky.

`useReducer` is an "additional" hook, and `useState` is the primary hook.

### How
The 4 things needed for `useReducer` are:
1. State - to be read
2. Dispatch function - to be called with case argument and payload(state related argument). This function is provided by the hook.
3. Reducer - this sets the new state based on the case argument and state related argument. This function is usually a switch case.
4. Initial value of the state.

The basic syntax for `useReducer` is:
```jsx
import React, { useReducer } from 'react';

function reducerFunc(state, action) {
	// latest state,
	// action is the variable passed to dispath
	switch(action.type)
	{
		case 'CASE_VAL':
			return {...state, name: action.payload}; // becomes state
		...
		default:
			throw new Error(`Unknown reducer type: ${action.type}`);
	}
}

function MyComponent () {

	const [stateVar, dispatchFunc] = useReducer(reducerFunc, intialState);
	
	return (<>
			...
			{state.name}
			...
			<button onClick={ ()=>dispatchFunc({type: 'CASE_VAL', payload: 'arg'}) }>Name<button>
			...
			</>);
}
```
About the syntax:
1. It's a convention to name the case argument 'type', and the state related argument 'payload'. It's not a rule though.
2. The reducer function is kept outside the component. This is not a very strict rule, but is the recommended way. Why: it doesn't re-prepare the reducer function every time that the component is run, which is good memory+time wise.

- Also, as in `useState`, dispatch causes a re-render of the component, with the new state.
- Having a `default` case (in the reducer function) that returns an error is a good practice, it helps avoid errors.

#### Computed initialState
- The `useReducer`, and hence `initialState` is ignored after the first render, the whole statement is.
- There is an alternative syntax, that's especially useful if the initial value is the result of an expensive computation, and so should be run once during the first render. Only the `useReducer` statement changes.
	```jsx
	const [stateVar, dispatchFunc] = useReducer(reducerFunc, intialArg, initFunc);
			// the initial value is now initFunc(initialArg).
	```

### What
- [Here](https://github.com/exemplar-codes/react-hello-world/blob/5a83a92598ad832fb882a43ede103946b9815458/src/Apps/UseReducerDemo/UseReducerDemo.jsx) is a simple example.
- `useReducer` is like having a signal + payload (action), an API(logic - reducer) and a backend (state). It's a good coding pattern. Makes the code sweet.
So `useReducer` is a syntax sugar of  `useState`, functionally.

[Here](https://devtrium.com/posts/how-to-use-react-usereducer-hook#what-is-react-usereducer-hook-and-how-to-use-it)'s a good article for useReducer I took info from.
