# 178. Using async await
Created Tuesday 19 July 2022

Make the request handler an `async` function and replace `.then` by `await`s. Example:
```jsx
import { useState, useEffect } from 'react';

const App() {
	const [data, setData] = useState(null);
	const [loading, setLoading] = useState(false);
	
	async function getProfile() {
		setLoading(true); // synchronous piece
		
		const response = await fetch('https://api.github.com/users/sanjarcode');
		const data = await response.json();
		
		setData(data); // synchronous piece
		setLoading(false); // synchronous piece
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
I have not completed learning about `async/await`, but it seems like replacing `.then` by `await` and using `try/catch/finally` blocks instead of `.catch`, `.finally` seems to work.