# 2. React Props
Created Sunday 06 September 2020

#### Why
React components should be reusable, so there's a need to associate data with a component, which it uses in rendering its JSX.

#### How
Everything in React is a component. And the whole UI is nothing but a tree of these components.
* An easy way to store data for a component is to store the data as key-value attributes of the component, just like HTML attributes.
* Only attributes passed to a component can be accessed by it, this is an organizing principle in React. The parent passes some of its data to child components as attributes. This is done for two reasons:
	* Reusablity: data changes the component behaviour, stuff that it renders.
	* Selected information: Every component should have as selective information as possible. This means that code does not have to subscript arrays or extract unnecessary hierarchy of objects. Makes the code simpler. Goal is to keep end information as *singular* as possible.
* Props are supposed to be **read-only**, this is to achieve separation of concerns. The logic for changing data should be carried out separately from the UI component. This lowers effort needed to write/debug components.

Note: Read-only property of props does not clash with React's philosophy of inherent coupling of final logic-expressions and UI code. The code to change props is not a final expression that is rendered. The final logic-expressions should be at-most logical operators and other short stuff.

#### What
Prop, short for properties, is a component's data storage object.
All data that a component works with is stored in this one object.

* Technically, prop is a key-value store based on the attributes (and values) provided by the parent component.

#### How to work with props?
* Passing data (props): To pass data to a child component, simply pass the data as attribute and values.
* Defining the component:
	* When writing a component that uses props, the **first parameter** in the component's function is the prop object.
	* This prop object can be **named anything** (if using a function based component, otherwise it's fixed, and called "props"), the only condition is that it must be the component function's first argument.
	* If the component is written as a class, it automatically has an object with **fixed name** "props".
* Accessing props: just use the props object as mentioned in the component function definition, via dot notation. Note that the attribute name should **match the key-name**. When using class component, just work with the props object.

Useful trick: An alternative to dot notation is to use ES6 destructuring, where the first argument can be a curly brace with props datum as comma separated objects.

Examples
```JSX
// Component file
function ChildComponent = (prop_obj) => {
  return (<div>
          	<h1> {prop_obj.names} </h1>
          	<h1> {prop_obj.date} </h1>
          </div>);
}

// Parent component passing prop to child component
function ParentToChildComponent = (props) => {
  return <ChildComponent names="Names" date="27 March" />
}
```
If using dot notation, the child component would look like this, concise.
```JSX
// Component file
function ChildComponent = ({names, date}) => {
  return (<div>
          	<h1> {names} </h1>
          	<h1> {date} </h1>
          </div>);
}
```
Class based component.
```JSX
class Welcome extends React.Component {
 render() {
   return <h1>Hello, {this.props.name}</h1>;
 }
}
```


