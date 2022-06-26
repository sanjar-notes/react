# 105. Portals
Created Monday 28 February 2022
- [ ] in vault

### Why
This construct helps in placing the resultant HTML code at a syntactically better place then it would usually be rendered. The React code still remains at the same place, but the final place as HTML code is changed.

Etymology: The HTML from the React code is placed (or "portaled") elsewhere.


### How
The location of the component's invocation remains unaffected (meaning it remains at its functional place, irrespective of the target HTML position, and can have props too), but in the component file, the component function returns `ReactDOM.createPortal(<MyComponentJSX />, targetElement)` instead of just the `JSX`.

- Note that the target element should be DOM node, i.e. the target element has to be added to `index.html`. So, it cannot be an element in a JS/JSX file.
- `ReactDOM.createPortal` also returns a component, which can be used elsewhere.


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
	return ReactDOM.createPortal(
		<div>
		...
		</div>
	), document.getElementById('portal-id');
};

export default MyComponent;
```

The place of use of the code doesn't get affected in any way.


#### Where is this useful ?
This is useful for things that need to rendered outside of the code components, but is tied to them - like modals (which need state-flipper and other props, but should ideally be placed just beside the root `div` of the React app).


### Note 1: Using a generic component for portaling stuff
Generally, when using a portal, there are 4 things:
1. The content
2. The generic component that will be portaled.
3. Portal destination, generally marked by a static `div` with `id` at top app level.
4. Invocation of the generic portal component, with content passed as prop/child.

The thing to note here is that there's no change to how this happens, as said on this page earlier.


### Note 2: Adding multiple components to portal destination
- Multiple components can be passed to the portal destination. This results in the components being appended after each other. For example, this is totally fine.
```jsx
import ReactDOM from 'react-dom';

const portalDestination = document.getElementById('portal');

function App() {
	return <>
		{ReactDOM.createPortal(<div>Hello 1<div>, portalDestination)}
		{ReactDOM.createPortal(<div>Hello 2<div>, portalDestination)}
	</>;
}
```