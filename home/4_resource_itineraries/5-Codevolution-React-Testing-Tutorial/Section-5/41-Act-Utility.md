# 41. Act Utility
Created Mon Sep 30, 2024 at 6:10 PM

[act](https://react.dev/reference/react/act) is helper to apply pending React updates before making assertions.

```jsx
const { result } = renderHook(useCounter, { initialProps: { initialCount: 0 } });
result.current.increment();
expect(result.current.count).toBe(1); // fails
```

```jsx
import { act } from "@testing-library/react";

const { result } = renderHook(useCounter, { initialProps: { initialCount: 0 } });

act(() => {
	result.current.increment();
});

expect(result.current.count).toBe(1); // passes
```

## Conclusion
When having code that causes state updates, RTL cannot wrap them with `act` automatically, so we need to do so manually.

This is specially relevant when testing hooks.