# 155. Preventing Unnecessary Re-Evaluations with React.memo()
Created Sunday 10 July 2022

### Why
- In the last page, we acknowledged that React when a component re-evaluates, so do all of it's constituents, even if their props haven't change (which includes not having any). This *is* inefficient.

### How
- The solution is simple, just compare the old and new props and run the component function only if there's a change. React provides this functionality out of the box.
- This optimization is a trade-off though - prop diffing vs function re-evaluation. 
	- And it depends (on number/complexity of props, number of child components) which is costly, so use `React.memo` with care.
	- If it's known that props will change frequently, it's better to avoid using `React.memo`.
	- It's better to use `React.memo` to avoid re-evaluations of whole UI tree sections, of course knowing that props don't change very frequently.
- Why isn't this 'prop-diffing' the default - because of the overhead of prop-diffing.

### What
Just wrap the component function, for which you want to do prop diffing of *received props*, with `React.memo()`. So, a normal component like this:
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
`React.memo` can also be used on components that don't receive props.