# 10. Persist across restarts
Created Sat Dec 30, 2023 at 1:56 PM

## Idea
Keep token in OS's secret manager (Android/ios), since app is completely killed when it closes.

Do not use AsyncStorage package, since its unencrypted. Instead use the 'expo-secure-storage' package. Available for both OS. Data is safe in OS's keychain.

## Using `expo-secure-storage`
```jsx
import * as SecureStorage from 'expo-secure-storage';

// API
await secureStorage.setItemAsync('someKey', 'valueIEAuthTokenString');

await secureStorage.getItemAsync('someKey');

await secureStorage.deleteItemAsync('someKey');
```

## Usage - App code
1. App root - get stored token and add to global state.
2. Root navigator - render "private" route if user (fetched data) is not null. Otherwise show public route, i.e. login screen.
3. API calls - add `Authorization: Bearer ${authToken}` using a request interceptor (axios). i.e. Send like cookie behavior.
4. 401 check - add a response interceptor (axios) that clears the fetched data (including auth tokens) if we get a 401 response (assuming we're not supposed to get one). Due to state change, the tree will re-render to the public route with an error message. Detail: Use Redux as a [service](https://redux.js.org/faq/code-structure#how-can-i-use-the-redux-store-in-non-component-files:~:text=however%2C%20there%20may%20be%20times%20when%20other%20parts%20of%20the%20codebase%20need%20to%20interact%20with%20the%20store%20as%20well.) to clear data, or normal dependency injection (by passing state and state setter to a util).
5. Logout - clear the data. Tree will re-render to the login page due to our route files.


```jsx
// request interceptor code
import axios from "axios";
const $axios = axios.create();

const appendCustomHeadersMiddleware = async (config) => {
	const getCustomHeaders = async () => { 
		return {
			// get token from keychain the keychain
			"Authorization": `Bearer ${await SecureStorage.getItemAsync(k.ACCESS_TOKEN)}`,
		};
	};
	const customHeaders = await getCustomHeaders();

	// add custom headers to existing headers
	Object.entries(customHeaders).forEach(([k, v]) => {
		config.headers[k] = v;
	});
	
	return config; // let the call start
};

$axios.interceptors.request.use(appendVpHeadersMiddleware);
```