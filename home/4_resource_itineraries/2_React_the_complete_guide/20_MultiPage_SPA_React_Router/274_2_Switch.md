# 274.2. Switch
Created Saturday 24 September 2022

## Why
I don't know. I guess, this is a way to have specificity.

Consider the following code (assume we don't wish to refactor):
```jsx
function App() {
  return (
    <>
	  {someCondition && (
        <Route path="/alice">
          <h1>Alice rendered someCondition</h1>
          <>...</>
        </Route>
      )}
      
      <Route path="/alice">
        <h1>Alice rendered</h1>
      </Route>
    </>
  );
}
```

Two cases:
1. If the `someCondition` is false, only the second one will render. OK.
2. If it's true, both will render. We don't want this to happen, i.e. we wish to render only first one.

### How
We need a construct that renders only the first matching `Route`.

Technically, we can iterate over the nodes using `for` a loop, `break` on route match. Or something similar.

## What
React Router v5 provides the `Switch` component which does exactly this.
Example - using code from above:
```jsx
import { Switch } from "react-router-dom";

function App() {
  return (
    <Switch>
      {someCondition && (
        <Route path="/alice">
          <h1>Alice rendered someCondition</h1>
          <>...</>
        </Route>
      )}

      <Route path="/alice">
        <h1>Alice rendered</h1>
      </Route>
    </Switch>
  );
}
```
This will select only the first matching child.

Note: Use only `Route` as children of `Switch`. Using general react nodes can cause confusion as they match with `/`.