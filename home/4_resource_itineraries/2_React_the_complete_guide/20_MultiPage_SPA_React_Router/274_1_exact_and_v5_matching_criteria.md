# 274.1. exact and v5 matching criteria
Created Saturday 24 September 2022

## v5 matching criteria
React Router v5 matching criteria is not very intuitive (i.e. it does not respect specificity). But it is simple:
```js
const matchingCriteria = () => url.startsWith(route); 

// kind of
// it's actually - "ancestor list prefix equals"
```

## Situation
The matching criteria leads to an issue. Consider the following code:
```jsx
function App() {
  return (
    <>
      <Route path="/alice">
        <h1>Alice rendered</h1>
      </Route>
      <Route path="/alice/bob">
        <h1>Alice/Bob rendered</h1>
      </Route>
    </>
  );
}
```
There are two cases. If the URL:
1. Is `/alice`, the first one matches, as it should. OK.
2. Is `/alice/bob`, the second one matches, as it should. But, the first one matches too, and so both get rendered.
  
We want to avoid this behavior, i.e. avoid the 2nd case.

## exact
`Route` has a boolean prop named `exact` which is used to solve this problem. Using the prop will render only if there's an "exact" match.

So, the code can be corrected to:
```jsx
function App() {
  return (
    <>
      <Route path="/alice" exact> <!-- render only on exact match -->
        <h1>Alice rendered</h1>
      </Route>
      <Route path="/alice/bob">
        <h1>Alice/Bob rendered</h1>
      </Route>
    </>
  );
}
```

## How
The `exact` prop is internally part of the criteria. After introduction of `Route.exact`, the criteria can be thought of as:
```js
const matchingCriteria = (exact) => exact ? url === route : url.startsWith(route); 
```

## Notes
This matching criteria issue can happen with all parts of React Router, e.g.`NavLink`'s activation. And so it supports the `exact`