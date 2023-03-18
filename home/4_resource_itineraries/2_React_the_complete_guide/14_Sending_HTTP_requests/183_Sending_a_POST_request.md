# 183. Sending a POST request
Created Tuesday 19 July 2022

### How
`fetch` can be used to make `POST` requests also. By default, it's `GET`.
To specify `POST`, a second argument is passed, along with `method`, `body` and `headers` (if needed).

Example:
```js
fetch(url, {
	method: 'POST',
	body: JSON.stringify(movie), // movie is an object, transformed into JSON
	headers: {
		'Content-Type': 'application/json',
	}
})
```

- The result of making a `POST` request depends completely on the API. It's not a strict requirement that `POST` create a new resource, which is the general convention.
- Similar to `GET` requests, we can add "Posting..." and error messages.
- Of course, we need to have a form to take in input.


### What
Except the second argument and a body, there's no difference between `GET` and `POST` code.