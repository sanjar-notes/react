# 161. Optimizing with useMemo
Created Thursday 14 July 2022

All optimizations we have spoken about till now (i.e. `React.memo` and `useCallback` hook) are about preventing unnecessary re-evaluations of *child components*. Now, we'll optimize computations inside a given component itself.

### Why
- Components will do computations on data, from parts of the props/context. 
- These computations can sometimes be expensive (time, space wise), and we would like to memoize them. Consider a general component:
```jsx
function MyComponent(props) {

	const ec1 = expensiveComp1(props.data1); // stores computation
	expensiveComp2(props.data2, props.data3); // returns void
	
	return <>...</>; // ignore, this, as we're focusing on component's own computations
}
```
Now, there's no need of optimizing component's self computations if :
1. It's the first evaluation.
2. If props have changed.

So there's scope for optimization only if some parts of the props (relevant to expensive computations) have not changed. In other words, we need to do something like `React.memo` (which works based prop diffing), but only check differences of certain props, and not all of them (`React.memo` does diffing of all).

### How
- React provides a way to selectively do prop diffing in order to avoid expensive computations - the `useMemo` hook.
- Syntax - wrap the computation in the hook along with a dependency array of props involved:
```jsx
import {useMemo} from 'react';

function MyComponent(props) {
	const ec1 = useMemo(() => {
		// ... computation involving
		return expensiveComp1(props.data1)
	}, [props.data1]);
	
	useMemo(() => { // void
		// ... computation involving props.data2, props.data3
		expensiveComp2(props.data2, props.data3)
		// not returning is fine
	}, [props.data2, props.data3]);
	
	return <>...</>;
}```
In short:
```jsx
function App(props)
{
	const computedValue = useMemo(() => {return /* computations */}, [/*props involved in the computation*/]);

	// OR, for void computations, don't assign, return anything
	return <>...</>;
}
```
- How does the hook work - just like `React.memo`, i.e. React keeps a copy of:
	1. latest relevant props (as indicated in the dependency array(s)) of the component instance.
	2. Latest evaluated value.
	Upon component re-evaluation, it executes the `useMemo` callback only if the indicated props have changed and updates the computed value. Otherwise it returns the previously computed value.
- Issues with reference values - consider the following code:
	```jsx
	import {useMemo} from 'react';
	
	function App() {
		return <Child list={[10, -2, 34, 2]} />;
	}
	
	function Child(props) {
		const sortedList = useMemo(() => props.list.sort(), [props.list]);
		return <>...</>;
	}
	```
	Suppose the UI tree evaluates. When `App` re-evaluates, it will cause re-evaluation of `Child`, but will it recompute `sortedList`? Yes, it will. Reason: `props.list` *has* changed, because when `App` was re-evaluated, it re-created the prop, and it won't be equal to stored prop (by the hook) because `Array` is not a primitive data type.

	How to solve this? Use `useMemo` in `App` (the parent) with an empty dependency array. This will ensure that the list is not re-created. The code will look like this
	```jsx
	import {useMemo} from 'react';
	
	function App() {
		return <Child list={useMemo(() => [10, -2, 34, 2], [])} />;

		// or, alternatively
		const list = useMemo(() => [10, -2, 34, 2], []);
		return <Child list={list} />;
	}
	
	function Child(props) { // no change needed
		const sortedList = useMemo(() => props.list.sort(), [props.list]);
		return <>...</>;
	}
	```
	Note: This kind of "data memoization" does have certain overhead.
	
### What
- Conditional execution with memoization of code based on selective prop diffing.


### Observations
- We can implement `React.memo` using `useMemo`, just pass the whole `props` object as the dependency and move the return value inside the callback. Example:
	```jsx
	const {useMemo} from 'react';
	const MyComponent(props) {
		const retValue = useMemo(() => {
			return <>...</>;
		}, [props]);
		
		return retValue;
	}
	```
- `useCallback` memoizes functions, but `useMemo` memoizes all kinds of data.

Assets
1. [Simple useMemo demo](https://github.com/exemplar-codes/assorted-reactjs-apps/commit/194d02dadc8d2dfa773ecf5915c19c75df307315)
2. [Parent Child useMemo demo](https://github.com/exemplar-codes/assorted-reactjs-apps/commit/04dbea03bac4309c617322451e9f5f32785d6c43)