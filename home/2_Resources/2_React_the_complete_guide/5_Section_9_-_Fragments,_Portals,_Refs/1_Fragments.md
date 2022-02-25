# 1. Fragments
Created Thursday 24 February 2022

#### `div` soup
- A function in JavaScript can ultimately return one object. This is OK, but leads to a not so good practice of wrapping sibling components in a parent containers like `div`s, even if it is not needed.
- This needs to be done in JSX, for JavaScript.
- It leads to something known as "`div` soup", i.e. many nested `div` inside each other in the final HTML rendered on the page, which are neither needed and don't provide any semantic structure.
<html></html>
The solution is to just create a wrapper component and return `prop.children` directly from it, without any JSX.

This hollow "Wrapper" component can then be easily used to wrap sibling components, without creating a "`div` soup". The Wrapper looks like this":
```js
// no need to import React, as no JSX is used.
function Wrapper(props) {
  return props.children;
}

export default Wrapper;
```
This can be used like so:
```jsx
return (<Wrapper>
		  <div>...</div>
		  <MyComponent />
		</Wrapper>);
```

#### React fragment
Instead of us always defining this hollow thing, React provides empty wrapper called "fragment".
It can be imported like so:
```jsx
import React, {Fragment} from 'react';
return (<Fragment>
		  <div>...</div>
		  <MyComponent />
		</Fragment>);
```
// OR to avoid explicit import:
```jsx
import React from 'react';
return <React.Fragment>
		  <div>...</div>
		  <MyComponent />
		</React.Fragment>);
```
but the **best way** is using empty angled brackets (this needs some setup, and is already configured with `create-react-app`).
```jsx
import React from 'react';
return (<>
		  <div>...</div>
		  <MyComponents />
		</>);
```