# 286. Working with Query Params
Created Saturday 01 October 2022

Query params have no affect on matching criteria.
- They are however, _available_ via React Router.
- In short, we need to _read_ qparams and do whatever we want with them. e.g. inside `useEffect`, for example.

## Why
Web standard.


## How
React Router can read/write query params. Implemented using the `location` object, perhaps.

## What
Access them on and do what you want.

### 1. Reading query params
We need to read the URL and then parse the query string.
1. We need to use `useLocation` hook (provided by React Router) to read the URL.
2. Then we pass the query params from step 1 into native JS `URLSearchParams`'s constructor.
3. Finally we extract the query param value from the `URLSearchParams` object using it's `.get` function.

Note: accessed query params are strings.

Example
```jsx
import { useLocation } from 'react-router-dom';

// URI: ?age=2
function App() {
	const location = useLocation();

	const qparams = new URLSearchParams(location.search);

	const age = qparams.get('age'); // we get 'age' as string, '2'
	
	return <h1>Age: {age}</h1>;
}
```
Note that URL params are accessible before page load, since URL determine the page (even in case of React Router, FIXME: (really, always??)).

### 2. Writing to query params
We used the `useHistory` hook to navigate to a different path.
It also works with query params.
There are two ways to do this:
- Set the string yourself, i.e.`history.push("..../?age=2")`
- Use `URLSearchParams` to create the query string, and push the formed string to `history.push()`. To create the query string, we also need the path, and so `useLocation` is also needed.

Example (manual string creation):
```jsx
import { useHistory } from 'react-router-dom';

function App() {
	const history = useHistory();
	
	const onClickHandler = () => {
		history.push("/list?sort=asc");
	};

	return <button>Sort asc</button>; // clicking will add '?sort=asc' to the URL
}
```

Example (proper string creation):
```jsx
import { useHistory, useLocation } from "react-router-dom";

function App() {
  const history = useHistory();
  const location = useLocation();

  const onClickHandler = () => {
    const qParamBuilder = new URLSearchParams();
    
    qParamBuilder.set("avatarEmoji", "😼");

    const updatedURL = location.pathname + "?" + qParamBuilder.toString();
    
    history.push(updatedURL); // clicking will add '?sort=asc' to the URL
  };

  return <button onClick={onClickHandler}>Sort asc</button>;
}

```

Note: The page re-renders on navigate, even if only query params are being (potentially) updated.