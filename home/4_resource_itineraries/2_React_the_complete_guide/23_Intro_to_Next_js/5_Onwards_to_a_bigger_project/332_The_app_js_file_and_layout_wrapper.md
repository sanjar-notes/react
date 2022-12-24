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

[Code - app-wide navbar](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/7020d006a5e22595b764213023efd2ee1d8a8101)

Note: A `router` prop is also passed to the component by Next.js, which is an object that contains the path, queryParam etc. This is because we cannot use `useRouter` here (why though, idk - FIXME). This may be used to conditionally alter/select layouts, page title, metadata etc based on route - which is better than doing it at each page.

## Extras - global styles
- Next.js recommends we put all "to be applied globally styles" inside the `_app.js` file only.
- CSS, SCSS and modules (for both) are supported by default in a  `create-next-app` app.
- All styles except in `_app.js_` will be scoped to the `default export` component in the file.

More info on styles, see the [docs](https://nextjs.org/docs/basic-features/built-in-css-support).