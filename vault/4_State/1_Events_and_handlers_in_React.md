# 1. Events and handlers in React
Created Saturday 22 January 2022

## Why
We have to attach and detach listeners to elements in vanilla JavaScript, which is an imperative style of programming.
But React's philosophy is to be declarative first. So events are handled differently.

## How
- All applicable events for different types of HTML elements are available as props on the HTML components.
- Events are named `onClick` or something named similarly (`on`+`EventName` in camelCase) in React. This way, no imperative `addEventListener` have to be attached.
- Note that the `onClick` (or similar prop) should only indicate the function name, instead of the whole code or a function call. Code-logic (because it's not an expression) should remain de-coupled from the UI (JSX) code.
Example:
```JSX
function OurComponent () {
	const clicked = () => { console.log('Clicked!!'); }; // de-coupled
	return <div onClick={clicked}> Hello </div>;
}
```

FIXME: read and explain here if needed - https://reactjs.org/docs/events.html