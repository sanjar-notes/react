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
- One dynamic param can match only one node of the route, i.e. `/users/:name` won't match `/users/1/sanjar` because `:name` cannot match two nodes `1` and `sanjar`.

Note: only descendants of a dynamic `Route` (i.e. a `Route` with a dynamic `path` props) can access dynamic params, the dynamic `Route` component itself cannot.

- The dynamic params are made available (using `useParams`) as an object. keys being name of dynamic param and values being the value as a `string`.

Example:
```jsx
function App() {
	console.log(useParams()); // won't work, blank {}. Reason: only descendants can access dynamic params
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


## Notes (edge case)
- If a descendant has multiple dynamic `Route` ancestors, the nearest ancestor dictates the dynamic route names (i.e. accessed params key names). Values remain the same of course.
    Example:
	```jsx
	function App() {
		console.log(useParams()); // won't work, blank {}. Reason: only descendants can access dynamic params
		return (
	      <Route path="/:username" exact>
			<AppChild /> <!-- gets username -->
		    <Route path="/:usernameX" exact>
		        <AppChild /> <!-- gets usernameX -->
		    </Route>
		    <AppChild /> <!-- gets username -->
	      </Route>
	  );
	}
	
	function AppChild() {
		console.log(useParams()); // will work
		return null;
	}
	```
	If possible, reuse a dynamic route param when setting a nested `Route` to avoid confusion. Example:
	```jsx
	function App() {
		return (
	      <Route path="/quotes/:quoteId" exact>
	        <AppChild />
	      </Route>
	  );
	}
	
	function AppChild() {
		const { quoteId } = useParams();
		
		return (
		      <Route path={`/quotes/${quoteId}/comments`} exact>
			    <!-- this is a static routes set dynamically, instead of using dynamic routes again-->
				<AppChildChild />
		      </Route>
		  );
	}
	```