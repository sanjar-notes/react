# 2. Portals
Created Thursday 28 February 2022
- [ ] in vault

### Why
This construct helps in placing the resultant HTML code at a syntactically better place then it would usually be rendered. The React code still remains at the same place, but the final place as HTML code is changed.

Etymology: The HTML from the React code is placed (or "portaled") elsewhere.


### How
The location of the React "code use" remains unchanged (meaning it remains at its functional place, irrespective of the target HTML position), but in the component file, the component function returns `ReactDOM.createPortal(<MyComponentJSX />, targetElement)` instead of just the `JSX`.


Effects (in comparison to un-portaled React code):
1. Data/props - nothing changes, as the place of use of the components doesn't need to change, only the source file changed.
2. Styles - remains the same. FIXME
3. State - works unchanged.

Example:
The code like this (i.e. at the source file):
```jsx
import React from 'react';

function MyComponent() {
	return (<div>
			...
			</div>);
};

export default MyComponent;
```
changes to:
```jsx
import React from 'react';
import ReactDOM from 'react-dom';

function MyComponent {
	return ReactDOM.createElement(
		<div>
		...
		</div>
	), document.getElementById('portal-id');
};

export default MyComponent;
```

The place of use of the code doesn't get affected in any way.


#### Where is this useful ?
This is useful for things that need to rendered outside of the code components, but is tied to them - like modals (which need state-flipper and other props), but should ideally be placed just beside the root `div` of the React app.