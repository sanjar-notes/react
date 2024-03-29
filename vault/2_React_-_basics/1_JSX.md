# 3. JSX
Created Thursday 27 August 2020

## Why
* React uses a declarative approach to code UIs. JSX makes this easy.
* JSX also makes the code 
	* Intuitive and readable, instead of function calls.
	* Both structure and structure-related-logic-**expressions (not all logic)** are kept together.
```JSX
function App() {
	const ul = document.createElement('ul');
	const li = document.createElement('li');
	
	ul.appendchild(li);
	li.appendChild(document.createTextNode('...'));

	return ul;
}
/* Same as
	<ul>
		<li>...</li>
	</ul>
*/
```
Just imagine, the verbosity and un-intuitiveness of similar code.

Actually, JSX behaves like this:
```jsx
<div className="intro">Hello, world</div>
// is equivalent to
React.createElement('div', {className: "hello"}, 'Hello, world' )
```
or as [JSX in Depth](https://reactjs.org/docs/jsx-in-depth.html) describes it:
> Fundamentally, JSX just provides syntactic sugar for the `React.createElement(component, props, ...children)` 

Note: React components are JavaScript functions, and are therefore supposed to return only one value. So, each component must have one and only one container. This is a disadvantage of JS, not of HTML.

## How
Handled by the Babel transpiler.

## What
* Short for JavaScript XML
* JSX is *not* necessary for using React, basic JS is fine too.
* JSX is a syntactic sugar for JavaScript, and so can be stored in variables.


### Rules for JSX
1. Like HTML except if specified otherwise.
2. Some reserved keywords are different:
	* ``className`` instead of ``class`` attribute.
	* ``htmlFor`` in HTML form `<label>` tag instead of ``for``.
3. JS **expressions** can be enclosed in braces {}. But avoid this, keep JSX lean - the logic outside JSX and result variable in JSX.
	```JSX
	function ExpenseItem(props) {
	  const month = 'March';
	  const day = 24;
	  return (<div>
			    <span> {day}th </span>
				<span> {month} </span>
			  </div>);
	}
	```
4. Components must start with a capital letter. Small letter indicates HTML element, and may lead to errors.
5. JSX is an expression too, so one can store it in a variable or return it.
6. JSX can restart inside JS, but still JSX and JS should be differentiated with a {} for the JS part. Simply remember that JSX is an object and it doesn't make sense to write objects after one another. Example:
	```JSX
	const day = 24;
	const month = 'March';
	return <div>{day}<span>th</span> {month}</div>;
	// 24th March
	```
7. `true`, `false`, `null` and `undefined` are rendered as empty whitespace. To really render them, convert to string first, like so `String(null)`.

See a gist of [more](https://flaviocopes.com/jsx/) rules.

### About JSX
* JSX prevents injection attacks - everything is converted into a string before being rendered.
* JSX represents objects.


