# 289 v5 Summary
Created Sunday 02 October 2022

0. Principle - change URL, everything else will happen automatically.

1. Routing constructs:
	1. There should be a root `BrowserRouter` parent.
	2. `Route` with `path` does conditional rendering w.r.t URL.
	3. Matching criteria is `url.hasPrefix(route)`.
	4. `Switch` for first matching render. `Route` has `exact` prop for exact match.

2. Links:
	1. `<Link to=""></Link>`. Prevent reload.
	2. `<NavLink to="" classes=""></Navlink>` gets highlighted when `to` is the same as current URL.
   
3. Read URL:
	1. Pathname - `useLocation` hook. `useLocation().pathname`.
	2. Dynamic path - `useParam` hook
	3. Query params, again `useLocation().search` into `URLSearchParams`.

4. Write to URL:
	1. `useHistory` for navigation.
	2. `useHistory` + `"?"` + `URLSearchParams.toString()` for query params.

5. Path strings - use strings or pass an object `{pathname: "", search: ""}`
