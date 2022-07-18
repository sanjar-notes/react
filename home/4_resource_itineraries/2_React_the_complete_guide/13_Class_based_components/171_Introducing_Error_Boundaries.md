# 171. Introducing Error Boundaries
Created Monday 18 July 2022

### Why
There are sometimes errors which are:
1. Used for informational purposes, i.e. error handling between different parts of an application.
2. Cannot generally be fixed. For example - if the server is temporarily not responding.

So why not use error handling normally? Well, if a child component throws an error, the `catch` should be inside the same component (and function). In short, it cannot be handled in a parent component.


### How
##### Error handling solutions
One way to do error handling is to create a context with error initialized to `null`. Then, instead of `throw`ing an error, we'll simply call a function (defined in this "error" context). The context provider will conditionally handle the error and show a message etc. See this [code](https://github.com/exemplar-codes/react-with-classes/commit/625ea216b0f7356c7039a03a7bfe13436407c04d).

This is, of course, not so elegant - we are having to import context, then call a function defined in it. A better way would be to just catch `throw`n errors directly by the kind of "error" context provider. This is possible if make changes to the React core library to catch error bubbling up from the source of `throw`.

React implements a functionally similar feature, called "Error boundary".


##### Error boundaries
- An error boundary is simply a *class* based React component that implements the `componentDidCatch` method. That's all. The error boundary also implements the usual `render` function.
- This error boundary wraps the app, or parts of it. When any of it's ancestor throws an error, the `componentDidCatch` method is called.
- When the error occurs, we should show some error UI. But we will first need to cause a re-render. To do that, we use state in the error boundary component. To cause the re-render, we mutate the state inside `componentDidCatch`. 
- When the error occurs, `componentDidCatch` gets called, where, as said, we mutate state to indicate that an error has occurred. In the next re-render the `render` method of the error boundary gets called, and we conditionally avoid the usual flow of the app, rendering a message component instead. By default the error boundary just render s`props.children`.
- The `componentDidCatch` has a parameter with the error that occurred available.

So, to add an error boundary to an app:
A. Create the class boundary
	1. Create a class based component with state indicating if an error has occured, and set it to `false`.
	2. Implement the `componentDidCatch` method so that it sets the state to specify that an error has occurred.
	3. Implement the `render` method to return `props.children` by default, and conditionally return an error component (or message).
B. Using the error boundary - wrap the potentially error causing part of the app by the error boundary (component).
C. You can now throw error by using `throw`.
That's all

Example - Consider the following app.
```jsx
import {Component} from 'react';
import MyUser from '.../path';

function App() {
	return <MyUser />;
}
```

```jsx
function MyUser() {
	return <button onClick={() => {throw new Error('Error occured');}}>Trigger Error</button>;
}

export default MyUser;
```

Let's define an error boundary to handle the error. Note, it must be a class based component:
```jsx
import {Component} from 'react';

class MyErrorBoundary extends Component {
	constructor() { // need state to cause a re-render when error occurs
		super();
		this.state = {hasError: false, error: null};
	}

	componentDidCatch(error) {
		this.setState({hasError:true, error: error});
	}

	render() {
		return this.state.hasError ? <p>Error Occured</p> : this.props.children;
	}
}

export default MyErrorBoundary;
```

To use the error boundary, wrap the potentially error causing component inside it. For example:
```jsx

function App() {
	return <MyErrorBoundary><MyUsers /></MyErrorBoundary>;
}
```

The error will now be caught.

##### A note about error boundary(s)
 - One may use multiple error boundaries and conditionally handle different types of errors, i.e. by using implementing `componentDidCatch` conditionally based on `error` parameter it provides.
 - Or use a single error boundary and use switch cases, with the state containing many types of "error has occurred".