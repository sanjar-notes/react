# 288. Writing more flexible Routing code
Created Sunday 02 October 2022

## Why
- We've been using hardcoded routes in the [practice app](https://github.com/exemplar-codes/react-router-practice). This is of course, not a good thing.
- Note that React Router still needs absolute URLs at all places (`Route.path`, `Link.to`), that doesn't change and is not a problem.
- We just want to minimize hardcoded stuff.


## How
If there was a way to get the URL for the parent `Route` in a component, we could use that to create URL to be used in the component (as React Router needs absolute paths at all times).

This way, even if we want to change the name of a `Route` higher up in the hierarchy, it would have no effect on any other `Route`s (above or below level).

Additionally, we can store each path node as a string variable, so we don't have to touch UI code, at all, even if route name changes.

## What
The `useRouteMatch` hook provides an object that contains the "matched" URL of the parent `Route`, and other info. We use it to create URLs.

Example:
```jsx
import { Route } from 'react-router-dom';

function App() {
	return <Route path="/welcome"><Child/></Route>;
}

function Child {
	const match = useRouteMatch();
	
	return <><h1>Previous route: {match.url}</h1></>;
}
```

## Path object instead of string (optional)
We are not hardcoding strings now, but we are still creating strings using `+`  or string interpolation.

There is a better way.

All the places where we have supplied strings, i.e. `Link.to`, `NavLink.to`, `Route.path`, `useHistory().push()` also accept an object, instead of a string. This object will be used to automatically create a string.

Example:
```jsx
const match = useMatchParams();

<Link to={{ search: "sort=true" }}>Sort</Link>;

<Link to={{ pathname: "/welcome" }}>Welcome page</Link> // replace URI

<Link to={{ pathname: match.url + "/welcome" }}>Welcome page</Link>



const history = useHistory();
const onClickHandler = () => history.push({ search: "sort=true" });
```

## Note
1. When creating paths using `useRouteMatch().url` and remaining path, `"/"` must be added in between.
2. While specifying route as object, the `pathname` still needs a prefix `/`. But having a `?` for query params is optional (has no effect).
3. `useRouteMatch()` also has the dynamic URL skeleton used by the parent, as well as the actual URL (which we have used) and the dynamic path params object.