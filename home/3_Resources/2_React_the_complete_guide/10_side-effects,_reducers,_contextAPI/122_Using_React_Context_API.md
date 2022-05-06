# 121. Using React Context API
Created Tuesday 14 March 2022
- [ ] in vault

### Why
Passing props or lifting state visibly is not good, better use a component-wide state.

### How
The 3 steps when using the Context API, obviously (logically), are:
1. **Create** the context. This is done in a standalone file.
2. **Provide** the context at the appropriate place (component). It's made available to all descendents of the selected root component.
3. **Consume** the context. Of course in a descendent.

There are two ways of consuming Context:
1. Using the `Consumer` component. This just looks a tad ugly.
2. Using the `useContext` hook. Looks good.

###### Details of using React Context
1. To **Create** the context, first make a React component called context. This is a JavaScript file. It's recommended to store this in a folder called 'store'.
```js
import React from 'react';

const AuthContext = React.createContext({});

export default AuthContext;
```
2. To **provide**, or place the store at the place of use - just import and wrap the context component (ContextComponent.`Provider`) around the ancestor component. This means that the context is available for all descendents, and the ancestor will re-render if any change occurs in the context.
   
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
3.  To consume the context, import the context component and use the `useContext` hook. Using the hook actually provides a read/write copy of the context, so that re-renders are possible (from the first ancestor).
```jsx
import React from 'react';

import AuthContext from './path_to_auth-context';

import AppComponent = () => {
	const ctx = useContext(AuthContext);
	
	return (<>
			{ 
			// can now read, write to ctx 
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
					// can now read, write to ctx 
					}
			}
			</AuthContext.Consumer>);
};
```

### What
- React context is thus a way to have a global state across components.
- The hook provides a read/write object for each user(consumer component). A write re-renders the parent component, effectively re-rendering all descendant components.

- One must be careful to not use context for reusable components, which must use props (which are basically arguments for them).
- So use context only when there's lot of plumbing needed AND for *specific* components.