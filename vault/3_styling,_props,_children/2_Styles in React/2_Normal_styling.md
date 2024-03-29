# 2. Normal styling
Created Sunday 13 February 2022

<https://speakerdeck.com/vjeux/react-css-in-js-react-france-meetup>

Let's continue with normal CSS analogues:
#### Inline style
Here the style is actually an object with key-value pairs for the styles. Hyphenated attributes must be camelCase and values must be string. Example:
```jsx
function Component(){
	return (<div style={{color: "red", backgroundColor: "blue"}}> ... </div>);
}
```

#### CSS in a file
Nothing changes in the CSS file, all types of selectors are possible in the CSS file. And id and classes can be used in JSX via `className` prop.

To use it, import the CSS file, like so:
```jsx
import './Component.css'; // imported
```
**Imported CSS file is not scoped to the existing component, and is applied globally.** So it's better to use classes on elements.

Now for the CSS features:
1. id - remains the same. Can be used on HTML elements only, not JSX elements. Of course, one may use id and trickle down the prop, but it's not advised.
2. class - is named as `className`, because `class` is a reserved keyword in JavaScript. Can be used on JSX elements too, but it needs to be properly appended as a prop on an HTML element. Like so
```jsx
import './Card.css';

function Card(props){
	return (<div className={'card ' + props.className}>
			...
			</div>);
}

// So we can do this
function FinalComponent(){
	return <Card className="button white bold"/>;
	// evaluates to class="card button white bold" for the div.
}
```
3. tag - available on HTML elements.