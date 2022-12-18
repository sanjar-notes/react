# 399. SSG for dynamic routes- `getStaticPaths`
Created Sunday 18 December 2022


## Why (situation)
We have a page with dynamic routes. But it's not that high velocity or variable data (for example the dynamic routes are movie names, and not something like social media post ID) 

Some of these routes are popular. So, we wish to build pages them before hand, i.e. we want to do SSG.

Also, we have a the list of popular movie names.

There are several problems:
1. Technically, issue with `getStaticProps` is that it runs only once, for a route.
2. We may not have "all" possible movie names. But we also don't want to do SSR (assume we don't have a very capable server).

So, SSG for dynamic routes. Also, we may not have a complete list of possible routes during build time.


## How
The solution is to run `getStaticProps` for all the dynamic routes that we want, for the given page.

For problem \#2, we could run `getStaticProps` on "request time" for movie names that weren't on our list, and store (like other SSG pages) the generated pages. So kind of a "memoized one time SSR".


## What
Next.js solves this problem, of SSG with dynamic routes, with the `getStaticPaths` function.

Similar to `getStaticProps` or `getServerSideProps`, it should be added (`expor`ted normally, technically speaking) page file.

Without `getStaticPaths`, the idea of a route param inside `getStaticProps` is moot, since it is run on build time, when no request exists.

With `getStaticPaths`, the "context" parameter in `getStaticProps` has a `param` attribute which is an object containing the dynamic route params. **Note**, this is not an array.

### Parameters
First one called "context". Contains the dynamic route param - again, an object exactly like `getServerSideProps`'s "context.param".

### Return value
The function must return an object with two things:
1. `paths` - an array with objects of shape `{ params: {paramOne: string, paramSecond: string, ... } }`.  Same as `getServerSideProps`'s "context.param".
2. `fallback` - boolean or the string `blocking`.
	- `false` - indicates that all paths have been listed. Returns 404 page for unlisted paths.
	- `true` - indicates that not all possible route params paths have been listed. On requests with a *new* unlisted path, Next.js responds to the client with a 'fallback' UI, but continues processing on the server - `getStaticProps` will be run with the requested route, cache the generated page and return it to the client, who will now see a fully loaded page. **In short, it's like `fallback.true` + new page returned**.
	- `'blocking'` - exactly like `true`, but instead of immediately returning a fallback page, responds only when the new unlisted route page is ready.

Note - in case of `fallback: 'blocking'`, `getStaticProps` runs once and the page component runs once. But in case of `fallback: true`, the component run once to generate the fallback UI (which is returned immediately to the client), then `getStaticProps` runs and then again the page component runs (this time with props).

Code examples - [`fallback:false`](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/57e80c86440f6345c43c51c3d524977fea72be6a), [`fallback:true`](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/3a8211464d693382f8f3214cd0b0655f75a00032), [`fallback:'blocking'`](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/91630a3607d47db45c7d3f37aaa649925e1e8806)

### Fallback pages
- The fallback page (used when `getStaticPaths` returns `fallback:true`) is specified inside the page component itself.
- To check if the page component is being run to generate fallback page, use `useRouter().isFallback`, which is a boolean.
- If `isFallback` is true, the UI returned by the page component is the fallback page.

Example:
```js
export default function MyPage() {
  const router = useRouter();
  if(router.isFallback) {
    return <MyLoadingSpinnerFallbackUI />; 
  }

  // page code
  
  return <...>; // return page UI as usual
}

export function getStaticProps() {
  //
  return ...;
}

export function getStaticPaths() {
  return { paths: [], fallback: true}; // or 'blocking'
}
```

Note: If `isFallback` is true, the page's props will be empty (as `getStaticProps` has been skipped to generate the UI). It will be available in the second run of the component, of course.

## Updating pages generated due to by `fallback: true` and `fallback: 'blocking'`
Both options are still a part of SSG, and hence they don't automatically update the pages they may have generated for unlisted routes.

To do so, use ISR, no special code required. i.e. in addition to returning `fallback` from `getStaticPaths`, also return `revalidate` from `getStaticProps`.