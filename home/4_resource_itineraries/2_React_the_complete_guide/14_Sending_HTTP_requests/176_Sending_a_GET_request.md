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
2. Also keep a "isLoading" variable, and use it to show some loading state, like an animation or text.
3. Use `useEffect` if request must be sent on App/component load. For event triggered fetches (like button clicks), there's no need to use `useEffect`. The event callback can do the network request.


### Extra
###### How to make requests with a time limit? (not discussed in course)
Well, it is simple. Use [axios](https://stackoverflow.com/a/62082804/11392807) for straightforward code.

If using fetch, do this:
1. Maintain an extra state "timeLimitExceeded" initialized to `false`.
2. Run the request (e.g. `fetch`) and a timer (with time limit) beside each other. Save this timer.
3. Nest this request and timer into a "void" promise, using `new Promise((resolve, reject) => ...)`. Resolve inside the network request, and reject with an error inside the timer.
4. Mutate "timeLimitExceeded" state to `true` in the catch clause of this promise. Add some UI element conditionally which displays an appropriate message.
5. In the `finally` clause, clear the timeout, using `window.clearTimeout`. Doing this to avoid running the timer if request was successful.
6. Nest this void promise inside a function.
7. Use this function in `useEffect` or as an event callback.

Code example:
```jsx
import { useState } from 'react';

function TimedRequestApp() {
	const [data, setData] = useState(null);
	const [loading, setLoading] = useState(false);
	const [timeLimitExceeded, setTimeLimitExceeded] = useState(false);

	const maxTimeLimit = 10000; // in millisecond
	
	function requestHandler() {
		setLoading(true);
		setTimeLimitExceeded(false); // remove existing message

		let limitTimer;
		new Promise((resolve, reject) => {
			limitTimer = setTimeout(() => {
				reject(new Error('Time Limit Exceeded'));
			}, maxTimeLimit)

			fetch(url).then(response => response.json()).then(data => {
				...
				// app-data logic
				...
			
				resolve();
			})
		})
		.catch(() => setTimeLimitExceeded(true))
		.finally(() => {
			setLoading(false));
			clearTimeout(limitTimer); // prevents execution if request successful
		}
	}
	
	return <>
			<button onClick={requestHandler}>Load Data</button>
			{loading && <p>Loading...</p>}
			{timeLimitExceeded && <p>Time Limit Exceeded! Try again</p>}
			{!loading && !timeLimitExceeded && data && JSON.stringify(data)}
		   </>;
}

export default TimedRequestApp;
```
Of course, we can also use `Promise.all`.