# 332. The `_app.js` file and layout wrapper
Created Wednesday 14 December 2022

## Why
There are many scenarios where we might want to control or wrap the whole app in a component.

It could be useful for _global_:
- Wrappers - layout, authentication wrapper, contexts, Redux's wrapper etc.
- Code -  code that runs for all pages from a single place.
  

## How
Let the user control the root component of the app. This way both code and UI (wrappers) can be added globally.


## What
Next.js exposes a simple way to wrap the whole app.

An optional `/pages/_app.js` file can be added which is supposed to be component that takes in two props named `Component` and `pageProps`, and returns the `Component` with `pageProps` as its prop.

- `_app.js` is present in the `create-next-app` scaffold, and deleting it is not an error.

Default `_app.js`:
```jsx
function MyApp({Component, pageProps}) {
	return <Component {...pageProps} />;
}

export default MyApp;
```

Adding global (to all pages) layout, modify `_app.js` to be:
```jsx
import Layout from '../components/path_to_layout_file';

function MyApp({Component, pageProps}) {
  return <Layout>
		  <Component {...pageProps} />
		 </Layout>;
}

export default MyApp;
```

Note: `_app.js` does is a helper page, and so does not take part in filename-routing (it still applies to all pages anyway).

## Extras - global styles
- Next.js recommends we put all "to be applied globally styles" inside the `_app.js` file only.

[Code - app-wide navbar](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/7020d006a5e22595b764213023efd2ee1d8a8101)