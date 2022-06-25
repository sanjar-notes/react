# 2. Rendering lists
Created Wednesday 09 September 2020

#### Why
React can render a hierarchied JSX object. But what about rendering **sibling** nodes.
React can render them too.

#### How
React render an array of JSX objects as sibling nodes.
Example
```JSX
return <div>{[<span> Hello </span>, <span> World </span>]}</div>
return <div>{names.map( (name) => <div>{name}</div> )} </div>} // commonly done
```

Note: React can render sibling nodes, but a single outermost container is still needed.
#### What
**How to output/render multiple components together on a page? Some approaches are:**
* Doing a for loop won't help, as it's not an expression, so no object will be rendered finally.
* A simple way to do this: Have an array of **JSX elements** in a div. All items in the array will be rendered as siblings, in order.

A simple way is to use **map** in JS, and this is used quite a lot.
e.g Making a list of components and, then rendering it
```jsx
const ninjaList = ninjas.map( 
	ninja => (<div>
				<div>Name: {ninja.name} </div>
				<div>Age: {ninja.age} </div>
				<div>Belt: {ninja.belt} </div>
			</div>));
return (<div> {ninjaList} </div>);	// render function
```
![](../../assets/pasted_image001%202.png)
*****
### Key attribute
* While rendering lists of components, React may redo the whole array even if only a single component is pre-pended in the latest UI frame. The reason being that React compares the lists in a simple iterative way. This can lead to bad performance.
- To avoid this bad performance, React can be given a hint via the "key" string attribute on the list JSX element (can be HTML element or custom, although in case key is passed to custom element it *won't* be available to it via prop).
- How does the "key" attribute help? React first compares key of a JSX element with all keys of existing list of JSX elements. If the key is present, React assumes the JSX elements are the same, so it ignores any updates for/inside them. This makes React fast, and also helps with cases like pre-pending an element, where performance without keys would be bad.
```jsx
<ul>
	<li> One </li>
	<li> Two </li>
</ul>

// vs - 3 thrashes. Bad performance.

<ul>
	<li> Zero </li>
	<li> One </li>
	<li> Two </li>
</ul>
```
```jsx
<ul>
	<li key="one"> One </li>
	<li key="two"> Two </li>
</ul>

// vs - Just a pre-pended component. Good performance.

<ul>
	<li key="zero"> Zero </li>
	<li key="one"> One </li>
	<li key="two"> Two </li>
</ul>
```
### Conditions for key
* The ideal candidate for the key attribute is the ID of the data being used. 
* A less and sometimes buggy candidate is the index of the array, as available in map (`map(vari, index)`). It is buggy because a JSX element would change internally, but have an ID same as existing nodes, this would not update the existing JSX, as it should, resulting in an error.
* An error shows if key is absent while rendering lists of JSX elements.
- Always use keys attribute for when rendering lists of JSX elements.
![](../../assets/Pasted_image_20220212185622.png)
- Keys should be unique only among siblings, and don't have to be globally unique.
* To remove the error, add the key attribute to each component being rendered.

```jsx
const ninjaList = ninjas.map( 
	ninja => (<div key={ninja.id}>
				<div>Name: {ninja.name} </div>
				<div>Age: {ninja.age} </div>
				<div>Belt: {ninja.belt} </div>
			</div>));
return (<div> {ninjaList} </div>);	// render function
```
