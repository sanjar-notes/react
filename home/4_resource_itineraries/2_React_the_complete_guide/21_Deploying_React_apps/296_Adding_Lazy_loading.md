# 296. Adding Lazy loading
Created Saturday 29 October 2022


## Why
Splitting code according to routes/pages/section or otherwise to reduce initial bundle size.

In other words, load stuff only when it's needed, i.e. lazy loading. This is implemented via "code-splitting".


## How
There are many constructs to specify lazy-loading in HTML, CSS, JavaScript and React.

- In React, entities (components, images, etc) are _loaded_ using `import`. And because the `import`s are usually done at file-level, outside of any function, it is effectively "eager loading" that we're doing.
- Conditional rendering of components, using bools or via routing doesn't help here, because even if a component (the function) isn't going to be rendered, `import`ing it will execute contents of it's file, thereby executing it's `import`s. This cascades further to all its dependencies. Example (`NestedComponent` is not rendered but still loaded`):
```jsx
import NestedComponent from '...'; // crux of the problem.

export default function App() {
  const isFetching = ...;
  
  return 
	<>
	  ...
	  {!isFetching && <NestedComponent />}
	  ...
	</>;
}
```
- This cascading effect is useful though, because if loading of a component is prevented, all it's dependencies are also prevented from loading.

To solve this issue, we need to prevent native `import` of entities we wish to load "lazily".


## What
To specify lazy loading in React, replace the `import` like so.
```jsx
// import NestedComponent from '.../path';
const NestedComponent = React.lazy(() => import('.../path'));
```
Doing this alone won't work. Reason: Dynamic import, i.e. `import()`, returns a `Promise` and so can be in the "pending" state.

Consequently, we need to provide a fallback UI (e.g. a loading spinner) which will be rendered when the lazily loaded component is being downloaded.

All this is done via the `Suspense` component provided by React, which accepts the fallback UI via the `fallback` prop.

```jsx
const NestedComponent = React.lazy(() => import('.../path'));

export default function App() {
  const isFetching = ...;
  
  return 
	<>
	  ...
	  {!isFetching && (
	    <Suspense fallback={<div>Loading...</div>}>
		  <NestedComponent />
	    </Suspense>
	  )}
	  ...
	</>;
}
```

One can lazy load any number of entities.

About `Suspense`:
- It's used in the JSX of a component that uses lazy loaded entities.
- The lazy component needs to be nested within it. It can be used at depth w.r.t the lazy component, either as a parent or ancestor.

FIXME, questions:
1. There's no way to associate `Suspense` with a lazy component, even if there are multiple lazy dependencies. In other words, each JSX block effectively has just one `Suspense`, and thus, custom fallback UIs for each cannot be specified.
2. Is their a way to associate a `Suspense` with lazy entity?

## Advice
Lazy loading is optional for small apps, but it's almost compulsory for large apps.

[See full code example](https://github.com/exemplar-codes/react-router-practice/tree/lazy_loading)