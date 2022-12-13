# 333. Programmatic navigation
Created Wednesday 14 December 2022

## Why
CSR programmatic navigation, since Next.js behaves just like an SPA after initial app load.


## How
Something like React Router's `.push()` (and other functions) would do.


## What
Next's `useRouter` hook (the object it returns on invocation) has methods to do programmatic navigation (CSR - without reload).

Example (can be done in reusable components or inside `/pages` - doesn't matter):
```jsx
import { useRouter } from 'next/router';

function MyPageOrComponent({id}) {
	const router = useRouter();

	const clickHandler = () => router.push(`/thing/${id}`);

	return <div>
			<button onClick={clickHandler}>Go to thing {id}</button>
		   </div>;
}
```

[Code - programmatic navigation](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/6981816e7c80c1fdf00e18dbe3d9af66d5a073ce)

Note - it is not a problem if we use `next` hooks and other features in components (i.e. non page ones). I thought it would be an issue if one wanted to use components from a Next app directly in a React app (without Next). But this is not a valid objection, since one would have to add stuff like `react-router` to implement CSR in a pure React project, because:
1. It (CSR routing) is not a standard.
2. There are many routing libraries.
3. React is a library, not a framework, and so it will always contain other code from libraries, and copying code from one React project to another which is differently configured (or uses different libraries) is not a practical idea (FIXME: OK, but to what extent is this idea helpful/doable?).