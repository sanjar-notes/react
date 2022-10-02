# 291. Upgrading to React Router v6
Created Sunday 02 October 2022

We learned about React Router v5 until now. It is significantly popular.

Changes:
1. v5.`Switch` is replaced by v6.`Routes` (plural).
2. `Route`s cannot be used in isolation, they must have a parent `Routes`. Ancestors are not enough.
3. Routing criteria has change it chooses the most appropriate route, i.e. specificity matters (and so `exact` has been deprecated) and wildcards are ignored if a specific matching route exists. <details><summary>More about the criteria (inside `Routes`)</summary>
	<ol>
		<li>Literal path</li>
		<li>Dynamic path</li>
		<li>Wildcard</li>
	</ol>
   </details>
4. Due to mandatory nature of `Routes` and new matching criteria, order of `Route`s is irrelevant.
5. v5.`Route` content are now passed as a prop (called `element`), and not as children.
6. `NavLink.activeClassName` has been deprecated. Instead, `style`/`className` prop must be used, which in addition to string/object(as usual), accept a function as prop, whose first param is `{isActive}`. This can be used to set the styles conditionally.
	```jsx
	function App() {
	  return (
	    <NavLink className={({ isActive }) => (isActive ? "active" : "")}>
	      Welcome
	    </NavLink>
	  );
	}
	```

Code examples (points 1-6) - [here](https://github.com/exemplar-codes/react-router-demo-v6).

FIXME: read, understand and clarify.
7. v5.`Redirect` is replaced by v6.`Navigate`. `Navigate` pushes the path to URL by default. Use the `replace` boolean prop to disable this behavior.
8. Nested `Route`s work only if the ancestor allows it, e.g. using a wildcard.
9. Paths should be relative to parent.
10. `Route` can have `Route` children. This is an alternative way to specify nested routes. When using this, we need to specify where a `Route` child should be rendered, using `Outlet` component provided by v6.
11. v5.`useHistory` is replaced by v6.`useNavigate` for programmatic navigation. 
	1. Push - `useNavigate()(path)`
	2. Replace - `useNavigate()(path, {replace: true})`
	3. Forward - `useNavigate()(positiveNumber)`. `1` for forward step.
	4. Backward - `useNavigate()(negativeNumber)`. `-1` for backward step.
	5. Refresh - `useNavigate()(0)`.
12. `Prompt` is not supported in v6. Solution: Create own Prompt component or use v5.