# 137. Adding a form
Created Saturday 25 June 2022

* Key attribute can be set on HTML elements as well as custom components. Note that key *won't* be available as prop if passed to a custom component. See [StackOverflow](https://stackoverflow.com/questions/30465651/passing-keys-to-children-in-react-js#comment-49012941) for details/discussion.

- It is normal and desirable to have a bunch of generic components that are used all over the app. They can be stored in a folder called 'shared' or 'UI'.

- `label` HTML element in React uses `htmlFor` instead of `for`.

- One can rewrite multiple attributes on an element succinctly, by using the spread operator. As usual, key-value of the object will match the attribute names and values.
```jsx
function App (){
	const attribs = {name: 'Sanjar', age: 24};
	return <>
		...
		<Item id={attribs.name} age={attribs.age} height={5.10}/> <!-- longer -->
		<Item {...attribs} height={5.10} /> <!-- equivalent, consise -->
		...
	</>;
}
```
