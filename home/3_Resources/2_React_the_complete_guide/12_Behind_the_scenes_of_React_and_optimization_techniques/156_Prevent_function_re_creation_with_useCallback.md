# 155. Preventing Unnecessary Re-Evaluations with React.memo()
Created Sunday 10 July 2022

### Situation - React.memo \*generally fails for functions received as props
\*exceptions - function returned by `useState`, or functions that are not re-created on re-component evaluation.

Consider this UI tree:
```jsx
import {useState} from 'react';

const Button = React.memo((props) => {
	console.log('Button ran');
	return <button onClick={props.toggleShow}>Click me!</button>
}); // using React.memo

const App = () => {
	const [show, setShow] = useState(true);
	
	const toggleShow = () => setShow(prev => !prev); // re-created on re-evaluation
	
	return (
			<>
				{show && <p> Text visible </p>}
				<Button toggleShow={toggleShow} />
			</>
		);
}
```

Will the `Button` be re-evaluated when it is clicked here? Yes, it will be, even if we use `React.memo`. This is because the prop passed to `Button` changes. Does it really? Yes, it is re-created on each re-evaluation in the `App`. Reason: functions are not primitive values, and therefore a change in reference (address in memory) means non-equality even if the values are the same. Some examples of this phenomenon:
```js
[1, 2, 3] === [1, 2, 3] // false, non-primitive variables are compared by address, in addition to value.
false === false // true, primitive values are compared by value.
```
- The function returned by `useState` is guaranteed to remain constant irrespective of re-renders.


### Why
The situation discussed above makes it impossible to use `React.memo` with usual in-component created functions (a.k.a callbacks).


### How
- React solves this problem by providing a hook that maintains the referential integrity of the callbacks between re-evaluations - the `useCallback` hook.
- To use it - wrap the callback function in `useCallback`, along with a dependency array (empty array is fine too). The callback used in the code example on this page can be re-written as:
	```jsx
	const toggleShow = useCallback(() => setShow(prev => !prev), []);
	```
- If anything in the dependency array changes, the callback function will be re-created on re-evaluation.
- When `useCallback` is used, React stores the callback function internally and keeps it independent of function re-evaluation, of course assuming that nothing in the dependency array changes.


### What
Use `useCallback` to make `React.memo` effective.