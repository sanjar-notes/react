# 164. What and why
Created Monday 14 July 2022

- Class based components are an alternative to function based components.
- Jargon - Class based components are also known as 'class components', the same goes for  function based components which are also known as 'function components'.
- With the exception of 'Error boundaries' - functional and class based components are equally valid for any kind of components, and are interoperable.
  
### Class vs function components - basic difference
![](../../../../assets/Pasted%20image%2020220714035506.png)
1. Functions return JSX directly. Classes need to have a function named `render` that returns the JSX.
2. Functions have `useState` for working with state which provides both the current value and a mutator for state. Classes store state as an instance variable named `state` and use the React provided mutator called `setState`.
3. Functions don't have to use the `this` keyword, almost always. Classes have to use `this` almost everywhere.
4. Functions use React "hooks" to hook into React life-cycle. Classes have "imperative" style hooks available to them. 
   *Note*: Classes cannot use React hooks, and Functions cannot use lifecycle methods (FIXME: not sure if functions cannot use lifecycle hooks).