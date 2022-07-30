# 231. Redux with React
Created Saturday 30 July 2022

[Code](https://github.com/exemplar-codes/react-redux-demo) - using Redux in React apps.

Need two `npm` packages for this project:
1. Core Redux - `redux`
2. React bindings in Redux - `react-redux`. This makes connecting React components to the store easier.

`react-redux`, in addition to other functions, helps in adding component re-render subscriptions to the store. Other than this, everything is already present in the `redux` package.

There are 4 things to keep in mind when using `redux` with `react-redux`:
1. **Store** - created using core `redux`. No change from core redux and React usage. Convention: stores are kept in a separate `.js` file.
2. **Provider** - `react-redux.Provider` is a wrapper component that should be wrapped around the UI sub-tree where store needs to be accessed. It takes a prop `store` which points to the redux store.
3. **Consuming** data from store, for functional components - use the `react-redux.useSelector` to access relevant part of the store. The first parameter is a function that takes in the store and returns the part of the store whose value is needed by the component.
4. For **dispatching** store changes in functional components - use the `useDispatch` hook which takes in the store as first parameter. It returns the store's dispatch function.

Subscriptions to components are automatically managed(i.e. added on component mount and remove on component dismount) by `react-redux`. In short, any change in the store will re-render relevant components in the UI sub-tree.


### Questions
How to access the correct state and dispatch function if there are multiple providers in the UI ancestor?? Neither `useSelector` nor `useDispatch` take a store as argument. I have observed that the innermost provider is chosen as the store state.