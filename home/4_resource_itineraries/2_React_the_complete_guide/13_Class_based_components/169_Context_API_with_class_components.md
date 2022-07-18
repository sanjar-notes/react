# 169. Context API with class components
Created Monday 18 July 2022

### What about context in class based components?
- Well, the *"context"* and the *"provider"* are *created* exactly the same way as with functional components.
- As for consuming the context, we can still use `MyContext.Consumer` and provided callback, exactly the same way as we did with functional component. Of course, this does not look good, and is undesirable, irrespective of whether the component is function or class based.

So, the only difference, is how we consumer context in a "good-looking way".
In functional components, we had the `useContext` hook, which could be used to access multiple contexts too. But class components don't have access to hooks.

***There's actually NO good way to access context, except the case when there's a single context.***

For consuming a single context, use the `static` modifier to indicate the context, like so:
```jsx
import {Component} from 'react';
import AuthContext from '.../path';

class MyComponent extends Component {
	static contextType = AuthContext;

	// Context is now available via this.context
}
```

If you need more than one context for a class component, one has to use a work-around.