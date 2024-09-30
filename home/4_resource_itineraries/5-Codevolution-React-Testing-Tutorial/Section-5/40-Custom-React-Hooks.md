# 40. Custom React Hooks
Created Mon Sep 30, 2024 at 5:43 PM

- File convention for hook remain the same. e.g. `useCounter.jsx` and `useCounter.test.jsx`.

## Why
Why is this a dedicated topic? 
- Hooks dont return JSX, so we cannot use `render`.
- Since hooks dont return `UI`, `screen` cannot be used for queries.


## What
The fix is to use `renderHook`. It returns a object, and `result` stores the result.

```jsx
import { renderHook } from "@testing-library/react";
// assume useCounter

const { result } = renderHook(useCounter);
const { result } = renderHook(useCounter, { initialProps: { age: 15 } ); // passing props
```

- [`rerender`](https://testing-library.com/docs/react-testing-library/api/#rerender-1) - `renderHook` exposes a `rerender` function.
	```jsx
	const { result, rerender } = renderHook(someHook, { initialProps: { age: 15 } });
	
	// re-render with changed value
	rerender({ age: 16 });
	```
- [unmount](https://testing-library.com/docs/react-testing-library/api/#unmount-1) - `renderHook` exposes a `unmount` function.
	```jsx
	const { result, rerender } = renderHook(someHook, { initialProps: { age: 15 } });
	unmount();
	```

## Example
```jsx
import { renderHook } from "@testing-library/react";
// assume useCounter

const { result } = renderHook(useCounter, { initialProps: { initialCount: 0 } });
expect(result.current.count).toBe(0);
```