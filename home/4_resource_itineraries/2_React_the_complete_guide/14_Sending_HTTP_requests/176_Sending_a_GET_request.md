# 176. Sending a GET request
Created Monday 18 July 2022

### Why
To make send/receive data from/to the server. We usually use HTTP (or HTTPS).


### How
- As a React app is fundamentally JavaScript code that runs in the browser, we can use browser APIs (like `fetch`) as well as HTTP request libraries (like "axios").
- We'll be using the built in `fetch` because it's supported by all browsers, as of now.

- Because network requests are handled asynchronously, we'll need to use state to cause a re-render when the request finishes.
- There are two cases for fetching:
	- Without `useEffect` - if fetch is triggered by the user or some other event.
	- With `useEffect` - need to fetch on app/component load.
  
Example of GET request - without `useEffect`, so using state:
```jsx
import { useState } from 'react';

const App() {
	const [data, setData] = useState(null);
	const [loading, setLoading] = useState(false);
	
	function getProfile() {
		setLoading(true);
		fetch('https://api.github.com/users/sanjarcode').then(response => response.json()).then(data => { setData(data); setLoading(false); });
	}

	return <>
			<button onClick={getProfile}>Load Data</button>
			<p>{loading && 'Loading...'}</p>
			<p>{!loading && data && JSON.stringify(data)}</p>
		   </>;
}

export default App;
```
Observe the flow of this component:
1. Initially, both data and loading are false.
2. Upon button click, the `getProfile` function is run. The first line (`setLoading(true)`) causes a re-render, but the function execution continues. The loading text is shown in this render.
3. `fetch` runs, and if assuming it's a success, causes state changes `setData(data)` and `setLoading(false)`. Both state changes are batched and the component re-renders. The loading text is now absent, and data is displayed.
Note: The most important thing here is that the callback function `getProfile` keeps running even if the component re-renders. This works because state mutators are guaranteed to remain unchanged on re-renders.

Similarly, we can make requests on App/component load, without a user event. To do so, use `useEffect`. Of course, we still need state to cause a re-render:
```jsx
import { useState, useEffect } from 'react';

const App() {
	const [data, setData] = useState(null);
	const [loading, setLoading] = useState(false);
	
	function getProfile() {
		setLoading(true);
		fetch('https://api.github.com/users/sanjarcode').then(response => response.json()).then(data => { setData(data); setLoading(false); });
	}

	const dataSignature = JSON.stringify(data); // to avoid infinite re-renders
	// need to stringify because object is a non-primitive data type
	
	useEffect(getProfile, [dataSignature]);
	
	return <>
			<p>{loading && 'Loading...'}</p>
			<p>{!loading && data && JSON.stringify(data)}</p>
		   </>;
}

export default App;
```

- We can avoid do requests without state too, by using `ref`s to update DOM on network request success, but we won't be able to show "Loading..." UI, which is very important for UX. So it's better to use state.


### What
To make network requests:
1. Use some state to render change on request success.
2. Use `useEffect` if request must be sent on App/component load. For event triggered fetches (like button clicks), there's no need to use `useEffect`. The event callback can do the network request.