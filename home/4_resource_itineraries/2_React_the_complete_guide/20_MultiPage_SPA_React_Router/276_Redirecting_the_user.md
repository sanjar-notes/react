# 276. Redirecting_the_user
Created Sunday 25 September 2022

## Situation
We want to redirect a user when they reach a certain URL.

## Why
Just needed.

## How
-

## What
Use the `Redirect` component of React Router.
```jsx
import { Redirect, Route } from 'react-router-dom';

function App() {
  return (
    <>
      <Route path="/" exact>
        <Redirect to="/login"/>
      </Route>
      
	  <Route path="/login">
        ...
      </Route>
    </>
  );
}
```
Here, if the user is at `/`, they automatically get redirected to `/login`. The `exact` is needed to prevent an infinite loop because `\login` matches both `Route`s.