# 42. Mocking Functions
Created Mon Sep 30, 2024 at 6:20 PM

## Why
Suppose a component takes onSubmit prop, and we want to make sure it gets called when some actions are done.

## How
A simple way is to keep a boolean (or number) and an array, send a dummy function that sets the boolean/increment the number to record number of times it was called, and with what all arguments.

After the act, we'll verify if it was called with the proper arguments.

`jest`/`vitest` provide such "mock" functions (that have attached metadata that the runner keeps track of). The runner also provides matchers that help in checking args and number of calls.


## What
```jsx
import { vi } from "vitest";
import user from "@testing-library/user-event";
// assume Counter, displays count, and has two buttons

const incrementHandler = vi.fn();
const decrementHandler = vi.fn();

renderHook(<Counter
	init={0}
	incrementHandler={incrementHandler}
	decrementHandler={decrementHandler} 
/>)

const incrementButton = screen.getByRole("button", { name: "Increment" });
const decrementButton = screen.getByRole("button", { name: "Decrement" });

await user.click(incrementButton);
await user.click(decrementButton);

expect(incrementHandler).toHaveBeenCalledTimes(1);
expect(decrementHandler).toHaveBeenCalledTimes(1);
```


## Important
Note that mocking functions is usually unconcerned with actual details of the operations.
All we wish to test here is that the function gets called the correct number of times and with the correct argument each time.