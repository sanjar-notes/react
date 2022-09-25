# 275. Nested routes
Created Sunday 25 September 2022

- This much simpler than it sounds.
- React Router can handle nested routes (e.g. `/welcome/get-started`) too.

- To do so, just keep the `Route.path` prop same as the whole route, i.e. `/welcome/get-started`.

## What
1. `Route` components can be nested within one another. Example:
	```jsx
	function App() {
		return (
		  <Route path="/alice">
			<Route path="/alice/bob" /> <!-- will be rendered on URL /alice/bob -->
		  </Route>
	  );
	}
	```
	As of now, nested `Route`s are "dumb", i.e. they don't remember their ancestor. Example:
	```jsx
	function App() {
		return (
		  <Route path="/alice">
			<Route path="/bob" /> <!-- won't work on URL: /alice/bob -->
			<!-- doesn't "know" who the parent is -->
		  </Route>
	  );
	}
	```
	**In short, the absolute `path` (i.e. URI from root) has to used at all places.**
3. The nested `Route`s inside a `Route` *don't* have to be semantically nested. Example - this is OK:
	```jsx
	function App() {
	  return (
		  <Route path="/welcome">
			<Route path="/products" /> <!-- not semantically nested but allowed -->
		  </Route>
	  );
	}
	```
4. If a `Route` doesn't match, none of it's children are rendered, even if they match. Example - consider the URL is `/products`:
	```jsx
	function App() {
	  return (
		  <Route path="/welcome"> <!-- doesn't match -->
			<Route path="/products" /> <!-- matches with URL, but not rendered, as parent does't match -->
		  </Route>
	  );
	}
	```