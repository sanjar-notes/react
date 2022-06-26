# 122. Using React Context API
Created Tuesday 14 March 2022
- [ ] in vault

### Why
Passing props or lifting state visibly is not good, better use a component-wide state.

### How
The 3 steps when using the Context API, obviously (logically), are:
1. **Create** the context. This is done in a standalone file.
2. **Provide** the context at the appropriate place (component). It's made available to all descendents of the selected root component. Remember to **specify** the context value (object) at this stage.
3. **Consume** the context. Of course in a descendent.

There are two ways of consuming Context:
1. Using the `Consumer` component. This just looks a tad ugly.
2. Using the `useContext` hook. Looks better.

###### Details of using React Context
1. To **Create** the context, make a React component named something like 'context'. This is done in separate a JavaScript file. It's recommended to store this in a folder called 'store'.
```js
import React from 'react';

const AuthContext = React.createContext({});

export default AuthContext;
```
2. To **provide**, or place the store at the place of use - import and wrap the provider component (i.e. ContextComponent.`Provider`) around the ancestor component. This specifies that the context will be available to all descendants, and the ancestor will re-render if any change occurs in the context.
   
   Remember to provide the context object here as a `value`.
```jsx
import React from 'react';

import AuthContext from './path_to_auth-context';

const AppCommonAncestor = () => {
	return (<AuthContext.Provider value={name: 'Unnamed'}> 
			{/* code as usual */}
			</AuthContext.Provider>);
};
```
3.  To consume the context, import the context component and use the `useContext` hook. Using the hook actually provides a read only<span title="write is achieved using functions, similar to lifting state up">*</span> copy of the context, so that re-renders are possible (from the first ancestor).
```jsx
import React from 'react';

import AuthContext from './path_to_auth-context';

import AppComponent = () => {
	const ctx = useContext(AuthContext);
	
	return (<>
			{ 
			// can read ctx. writing is done by function invocation
			}
			</>);
};
```

Note: There's another way to consume context - just wrap the consuming component's code by the Context.`Consumer`. This is equivalent to using the hook, but looks bad.
```jsx
import React from 'react';

import AuthContext from './path_to_auth-context';

import AppComponent = () => {
	return (<AuthContext.Consumer>
			{ 
				(ctx) => {
					// can read ctx. writing is done by function invocation
					}
			}
			</AuthContext.Consumer>);
};
```

Tip: For better IDE auto-completion, just add some attributes (called default context) in the context component.

### What
- React context is thus a way to have a global state across components.
- The hook provides a read only object for each user(consumer component). A write re-renders the ancestor component, effectively re-rendering all descendant components.

- One should absolutely use `useState`, `useEffect` at the component where context is "Provided", for persistence and automatic re-renders, of course by adding the `useState` variables to the context. FIXME: is `useState` even required if writing to context already causes re-render?

- One must be careful to not use context for reusable components, which must use props (which are basically arguments for them).
- So use context only when there's lot of plumbing needed AND the components involved are *specific*(i.e. not reused).

- Context component(s) and the store folder are nice way to handle all data within the app, in a dedicated place.

### Architectural style for context
There are two ways to write code when using context:
1. Have a file containing the context, and specify the provider at the "root" (ancestor) of the UI subset. The stateful logic, in this case is specified at the "root" component, and is accessible within the same file.
	```jsx
	// FoodContext.js
	const FoodContext = React.createContext({});
	export default FoodContext;
	```
	```jsx
	// FoodRoot.jsx
	import FoodContext from './store_path/FoodContext';

	function FoodRoot () {
		// whole tree's state logic start
		const [count, setCount] = useState(0);
		// state logic end

		return 
		(
			<FoodContext.Provider value={{count, setCount}}>
				... <!-- can use count, setCount here -->
			</FoodContext.Provider>
		);
	}
	export default FoodRoot;
	```
2. Have a single file to specify both the context and provider (use `props.children` here), and export both. Essentially, all context (including state logic) resides in the context file, and not in any core UI component. Note that the context is not available at the "Provider" component ("FoodRoot.jsx" here).
	```jsx
	// FoodContext.js
	const FoodContext = React.createContext({});

	function FoodContextProvider() {
		const [count, setCount] = useState(0); // have state logic here

		return 
		(
			<FoodContext.Provider value={{count, setCount}}>
				... <!-- can use count, setCount here -->
			</FoodContext.Provider>
		);
	}
	
	export default FoodContext;
	export { FoodContextProvider };
	```
	```jsx
	// FoodRoot.jsx
	import { FoodContextProvider } from './store_path/FoodContext';

	function FoodRoot () {
		return 
		(
			<FoodContextProvider>
				... <!-- CANNOT use count, setCount here -->
			</FoodContextProvider>
		);
	}
	export default FoodRoot;
	```

- Note that both styles don't affect the consumption of the context in any way, and that we still need to export the context.
- What to use? Well both have their pros and cons. In case 1, context is available in the "Provider" component, but not in case 2. The con of case 1 is that the Provider is clogged with context details, which may be removed from it and placed in the context, to make the code lean.