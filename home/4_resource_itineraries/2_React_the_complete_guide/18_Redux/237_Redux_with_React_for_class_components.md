# 237. Redux with React for class components
Created Saturday 30 July 2022

There are 5 things when using `redux` with `react-redux`:
1. **Store** - creation is same as with functional components.
2. **Provider** - same as with functional components.
3. **Consuming** data from store, for class components - all data to be consumed is provided through props. We have to define a function, by convention called "*mapStateToProps*" which takes in the store state as argument and must return an object of to-be-props pointing to relevant parts of the store state. This object will be added to existing props of the component. Example:
	```jsx
	function mapStateToProps(state) {
		return { count: state.count, showCount: state.showCount };
	}
	```
4. **Dispatching** store changes in class components - this is also done by adding functions to props. One needs to define a function, by convention called "*mapDispatchToProps*" which provides the dispatch function of the store as it's first argument. We must return an object of to-be-added-props which help in mutating the store. There are two ways to do this - pass the dispatch function itself as a prop, or create functions which call the dispatch function, and are called from inside the component. Example:
	```jsx
	function mapDispatchToProps(dispatch) {
		return { 
			incrementHandler: () => dispatch({type: 'INCREMENT'}),
			toggleCountHandler: () => dispatch({type: 'TOGGLE'})
		};
	}

	// OR
	
	function mapDispatchToProps(dispatch) {
		return { dispatch };
	}
	
	class MyComponent extends React.Component {
		incrementHandler() {
			this.props.dispatch('INCREMENT');
		}
		
		toggleCountHandler() {
			this.props.dispatch('TOGGLE');
		}
		render(){ /*  */}
	}
	```
5. **Connecting** the consumption and dispatch functions to the component. This is done by the `react-redux.connect` function. It is a function that takes in the "*mapStateToProps*" and "*mapDispatchToProps*" functions as arguments and return s an HOC function that takes the React component as argument, and returns the component with the props attached. See:
	```jsx
	import {connect} from 'react-redux';
	
	class MyComponent from React.Component {
	}

	function mapStateToProps() {}
	function mapDispatchToProps() {}

	export default connect(mapStateToProps, mapDispatchToProps)(MyComponent);
	```
   
Subscriptions to components are automatically managed(i.e. added on component mount and remove on component dismount) by `react-redux`. In short, any change in the store will re-render relevant components in the UI sub-tree.

Note: 
1. In both *mapStateToProps* and *mapDispatchToProps*, we only have to return an object of props to be added. Existing props are merged with this object.
2. Both *mapStateToProps* and *mapDispatchToProps* have latest (really?, FIXME) props available to them as the second parameter. i.e.:
	```jsx
	function mapStateToProps(state, props) { return {}; }
	function mapDispatchToProps(state, props) { return {}; 
	```
3. `connect` works for functional components too. So this way of consuming and dispatching may be used by functional components too. This works because the a functional or class component, is essentially the same and `connect` doesn't care. So, this, works too:
	```jsx
	import {connect} from 'react-redux';
	
	function MyComponent(props) {
	}
	
	function mapStateToProps() {}
	function mapDispatchToProps() {}
	
	export default connect(mapStateToProps, mapDispatchToProps)(MyComponent);
	```
	This way is sometimes preferred because it separates real props from store props.

### Questions
How to access the correct state and dispatch function if there are multiple providers in the UI ancestor? Neither `mapStateToProps` nor `mapDispatchToProps` take a store as argument. I have observed that the innermost provider is chosen as the store state.