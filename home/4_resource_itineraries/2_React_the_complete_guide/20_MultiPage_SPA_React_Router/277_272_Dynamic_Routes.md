# 277.272 Dynamic Routes
Created Sunday 25 September 2022

React Router allows for dynamic routes, to allow for something like `github.com/sanjarcode` to be generalized as `github.com/:username`.

This `:paramName` syntax is used inside `Route.path`.

Example:
```jsx
function App() {
  return (
    <>
      <Route path="/" exact>
        Landing page
      </Route>
	  <Route path="/:username">
        Your page
      </Route>
    </>
  );
}
```
Of course, we don't have the value of username here.
Let's get it.

## Accessing dynamic params
- Dynamic params of a `Route` are made available to all descendant components. All get the same params, irrespective of depth.
- To access them, use the `useParams` hook inside a descendant component.
- One can have a mix of dynamic and non-dynamic route nodes. e.g. things like `/home/:username`, `/:username/:repository` or `/:username/settings` are all OK.
- One dynamic param can match only one node of the route.

Note: only descendants of a dynamic `Route` (i.e. a `Route` with a dynamic `path` props) can access dynamic params, the dynamic `Route` component itself cannot.

Example:
```jsx
function App() {
	console.log(useParams()); // won't work, blank {}. Why: only descendants can access dynamic params
	return (
      <Route path="/:username" exact>
        <AppChild />
      </Route>
  );
}

function AppChild() {
	console.log(useParams()); // will work
	return null;
}
```