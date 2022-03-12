# 117. useReducer hook
Created Tuesday 12 March 2022
- [ ] in vault
    
### Why
`useReducer` is kind of a syntax sugar (FIXME: is it really, or close to) for `useState` . It is preferred if:
1. The state is complex and has many parts.
2. Goal state depends on the previous state.

- `useReducer` is an "additional" hook.
### How
4 things needed for useReducer are:
1. State - to be read
2. Dispatch function - to be called with case argument and state related argument.
3. Reducer - this sets the new state based on the case argument and state related argument.
4. Initial value of the state.

The basic syntax for `useReducer` is:
```jsx
import React, { useReducer } from 'react';

function reducerFunc(state, action) {
	// latest state,
	// action is the variable passed to dispath
	switch(action.argVal)
	{
		case 'CASE_VAL':
			return {...state, name: action.argVal}; // becomes state
		...
		default:
			return state;
	}
}

function MyComponent () {

	const [stateVar, dispatchFunc] = useReducer(reducerFunc, intialState);
	
	return (<>
			...
			{state.name}
			...
			<button onClick={ ()=>dispatch({type: 'CASE_VAL', argVal: 'arg'}) }>Name<button>
			...
			</>);
}
```
About the syntax:
1. It's a convention to name the case argument 'type'. It's not a rule.
2. The reducer function is kept outside the component. This is not a very strict rule, but is the recommended way. Why: it doesn't re-prepare the reducer function every time that the component is run, which is good memory+time wise.

Also, as in `useState`, dispatch causes a re-render of the component, with the new state.

#### Computed initialState
- The `useReducer`, and hence `initialState` is ignored after the first render, the whole statement is.
- There is an alternative syntax, that's especially useful if the initial value is the result of an expensive computation, and so should be run once during the first render. Only the `useReducer` statement changes.
```jsx
	const [stateVar, dispatchFunc] = useReducer(reducerFunc, intialArg, initFunc);
	// the initial value is now initFunc(initialArg).
```
### What
[Here](https://github.com/exemplar-codes/react-hello-world/blob/5a83a92598ad832fb882a43ede103946b9815458/src/Apps/UseReducerDemo/UseReducerDemo.jsx) is a simple example.

So `useReducer` is like a syntax sugar (FIXME: is it like, or totally?) of  `useState`, functionally.