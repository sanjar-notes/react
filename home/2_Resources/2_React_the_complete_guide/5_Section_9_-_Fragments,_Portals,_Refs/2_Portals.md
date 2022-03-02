# 2. Portals
Created Thursday 28 February 2022
- [ ] in vault

### Why
This construct helps in placing the resultant HTML code at a syntactically better place then it would usually be rendered. The React code still remains at the same place, but the final place as HTML code is changed.

Etymology: The HTML from the React code is placed (or "portaled") elsewhere.


### How
The location of the React code remains unchanged (meaning it remains at it's functional place, irrespective of the target position), but in the component file, a function returning `ReactDOM.createPortal(<MyComponent />, targetElement)` declared, and this function is actually used as the component name for the React code destination element.