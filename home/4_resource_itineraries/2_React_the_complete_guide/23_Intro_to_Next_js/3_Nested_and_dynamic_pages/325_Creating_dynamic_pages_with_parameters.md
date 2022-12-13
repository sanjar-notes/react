# 325. Creating dynamic pages with parameters
Created Wednesday 7 December 2022

## Situation
Suppose we need a page like `/users/{username}` where the `username` is dynamic.

Creating files like `/users/sanjar.js`, `/users/mike.js` and so on for all possible usernames would not be practical.


## Why
We need something like a dynamic route, and a way to use it with file-based routing.


## How
Next.js has a simple solution. Use square brackets for of the route parameter part of the route.
- Skeleton - `pages/pageName/[id].js` which routes to `pageName/{id}`.

Examples (request route <=> file in `pages/`):
- `/{id}` - `[id].js`
- `/news/{newsId}` - `/news/[newsId].js`
- `/users/{id}/details` - `/users/[id]/details.js` (yes, dynamic routes can have child routes and so can be used as folder names).


## What
There's no special code needed for this feature. [See code](https://github.com/exemplar-codes/nextjs-first-tutorial/commit/4b41e163dbf3291e809eb2fe8b2a0fd396969723)

Accessing the route param is crucial for most pages, especially for data fetching during a pre-render.

Next.js being a framework, has routing functionality (`next/router`) built into it.

### Reading the route param
The route param is read using the `useRouter` hook provided by React. It returns an object with shape 
```js
{ 
  query: { [routeParamName]: '_routeParamValue_' }
}
```

Example - `news/[newsId].js` page:
```jsx
import { useRouter } from 'next/router';

export default NewsDetail()
{
	const router = useRouter();
	
	const id = router.query.newsId; // IMPORTANT: same name as used in file name

	const newsDetails = ...; // fetch data from backend, if needed

	return <div>...</div>;
}
```

[Accessing dynamic route params - code](https://github.com/exemplar-codes/nextjs-first-tutorial/commit/5d9ec2136c1676d927f4f0b5f07b73b5227af514)