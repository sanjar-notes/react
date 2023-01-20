# 155. Preventing Unnecessary Re-Evaluations with React.memo()
Created Sunday 10 July 2022

### Why
- In the last page, we acknowledged that in React, when a component re-evaluates, so do all of it's constituents, even if their props haven't change (which includes not having any). This *is* inefficient.

### How
- Solving the problem
	- The solution is simple, just compare the old and new props and run the component function only if there's a change. If there's no change, return the stored copy of the render output, i.e. don't compute it again. React provides this functionality out of the box.
	- This optimization is a trade-off though - prop diffing vs function re-evaluation. 
		- And it depends (on number/complexity of props, number of child components) which is costly, so use `React.memo` with care.
		- If it's known that props will change frequently, it's better to avoid using `React.memo`.
		- It's better to use `React.memo` to avoid re-evaluations of whole UI tree sections, of course knowing that props don't change very frequently.
	- Why isn't this 'prop-diffing' the default - because of the overhead of prop-diffing.
- **Important note** - `React.memo` is only concerned with props. State changes will always cause a re-evaluation, `React.memo` has no control over that.


## What (syntax and details)
 - Skeleton - `export default React.memo(Component, [areEqualCallback])`

### Basic usage
- Just wrap the component function, for which you want to do prop diffing of *received props*, with `React.memo()`. So, a normal component like this:
	```jsx
	const MyComponent = (props) => { return <> ...</>; };
	
	export default MyComponent;
	```
	becomes
	```jsx
	import React from 'react'; // cannot be skipped if using memo
	const MyComponent = (props) => { return <> ...</>; };
	
	export default React.memo(MyComponent);
	
	
	// OR equivalently
	const MyComponent = React.memo((props) => { return <> ...</>; });
	
	export default MyComponent;
	```
- `React.memo` can also be used on components that don't receive props.

### Custom diff usage
- Intent - the following construct is provided by React because it only does "shallow" comparison of props, i.e. only checks if the reference has changed or not. This is not sufficient at all, since props are objects. Even if there are no props, the props value if `{}`, and `{} === {}` is false in JavaScript.
- The second argument of `React.memo` is optional. It's a function.
- Parameters: previous and current (new) props, in this order.
- Return value specifies if function should re-run (and potentially re-render) or not. So:
	- `true` - don't run
	- `false` - do run
- By default it returns false.

Example:
```jsx
const MyButton = React.memo(
  ({ title }) => {
    const clickHandler = () => window.alert("Hello");
    
    return <button onClick={clickHandler}> {title} </button>;
  },
  (prevProps, curProps) => prevProps.title === curProps.title
);
```


## MAid
`useMemo` helps us prevent re-evaluations of components when the app tree re-renders. Additionally, it can do this w.r.t props.


## Thoughts
- The prevent re-run with component without props case should be default behavior. [More info](https://stackoverflow.com/questions/53074551/when-should-you-not-use-react-memo).
- How does the hook work? My guess:
	- React keeps a copy of two things internally:
		- Props received in the latest evaluation.
		- Return value of the latest evaluation.
	- If props have changed, it re-evaluates the function and stores both props and return value. And returns the return value to the parent.
	- If props haven't changed, it just returns the stored return value of the latest evaluation to the parent.
	- Note: the return value is stored "kind of" in the component itself (which was wrapped in `React.memo`), and not it's parent. This means that the parent is oblivious to the fact that it received a stored value instead of a newly computed one. FIXME(I'm not sure if the both props and return value are stored in the parent or not. Also need to find out if the parent knows if one of it's children value was a stored value, not a computed one, maybe the parent is aware, idk)
- How to control re-evaluation w.r.t both state + props? FIXME (this was popular in class components). BTW: I never had to do this, during experiments or work, atleast knowingly. How would I do it without a new hook, approaches:
	1. State changed, there are no props. FIXME: continue later: https://codesandbox.io/s/angry-agnesi-4e4be2?file=/src/App.js. Also see [discussion on bailing out of state upates](https://github.com/facebook/react/issues/14110) - I actually encountered this somewhere in the Redux section, oh, [here](obsidian://open?vault=reactjs-notes&file=home%2F4_resource_itineraries%2F2_React_the_complete_guide%2F25_Replacing_Redux_with_React_hooks%2F372_Alternative__using_the_Context_API). 
	```jsx
	function stateComparator(prevState, currentState) { // true means don't re-evaluate
		return ...; // some diffing logic
	}
	
	function MyShell() {
		const [command, setCommand] = useState("App initialized");
		
		return <div>
			<input onChange={(e) => setState(e.target.value} value={command} />
			<br /> <span>{command}</span></div>;
	}
	```