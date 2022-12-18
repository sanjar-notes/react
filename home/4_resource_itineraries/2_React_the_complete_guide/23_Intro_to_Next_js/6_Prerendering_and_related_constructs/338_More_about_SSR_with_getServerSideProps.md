# 338. More about SSR with `getServerSideProps`
Created Sunday 18 December 2022

## General details
- We know that `getServerSideProps` is the way to do SSR in Next.js. It runs on every request.
- It returns an object with a `props` attribute whose value is an object of props to be consumed by the page component. Example:
```js
export default function MyPage({name}) {
  return ...;
}

export function getServerSideProps() {
  // run server side code
  
  return {
    props: { name: 'Sanjar' }
  };
}
```
- Returning `revalidate` does not work with `getServerSideProps`, since SSR, by definition runs on each request.


## "context" parameter
`getServerSideProps`'s first parameter is called "context".

It's an object that has many useful attributes, like:
1. **Dynamic route params** - an object with dynamic attributes as attributes and their values as strings. Examples params (page, request URL --> param):
   - `/pages/[id].js`, `/sanjar` --> `{ id: 'sanjar' }`
   - `/pages/help/[verb].js`, `/help/turning-off` --> `{ verb: 'turning-off' }`
   - `/pages/[country]/[name].js`, `/in/sanjar` --> `{ country: 'in', name: 'sanjar' }`.
   
	Code example (`/pages/help/[verb].js` and `/help/cleaning`):
 ```js
 export default...// page component here

 export function getServerSideProps(context) {
   const params = context.params;
   const verb = params.verb; // `cleaning`

   // run server side code
   
   return { props: {...} };
 }
 ```
2. **Request, response** - Since `getServerSideProps` runs for each request, it has access to the [request](https://nodejs.org/api/http.html#http_class_http_incomingmessage) and [response](https://nodejs.org/api/http.html#http_class_http_serverresponse) HTTP params, similar to Express.js. Both are present in the 'context' parameter of `getServerSideProps`. Example:
```js
// page component

export function getServerSideProps(context) {
	const { req, res } = context;
	
	// run server side code
	
	return { props: ... };
}
```
	Can we respond with the response object?? Probably not. FIXME
3. **Query params** - An object representing the query string, including dynamic route parameters. All values are strings. Examples:
	- `/pages/help.js` with URL `/help?chatId=23` --> `{ chatId: '23'}`
	- `/pages/[user].js` with URL `/sanjar?admin=yes` --> `{ admin: 'yes', user: 'sanjar'}`
4. **Cookies** - the request object has an additional attribute, called `cookies`, which is an object with string keys mapping to string values of cookies.


## Return value
The function must return a non-empty *object*. Attributes:
1. `props` - props for the page component, must be an object. So `{ props: {} }` is the minimal return value.
2. `notFound` - boolean. True returns the 404 page.
3. `redirect` - send a redirect response. Shape - `{ destination: string, permanent: boolean }`. Destination can be internal or external. For old HTTP clients, send a `statusCode` attribute, and omit `permanent`.

[Simple code example](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/87f32ea191fa16e12e7641cd7ecea0489b452e4a)
[More realistic code example](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/7e75f3024dd337914382b4fa77d5a00ab9a153bf)

## When to use SSR
Prefer SSG, then ISR if it's possible - if data velocity is slow, or the page doesn't need real time updates, like a blog.

Use SSR - data velocity is high (for a dashboard page, for example) or need access to request and/or response object.