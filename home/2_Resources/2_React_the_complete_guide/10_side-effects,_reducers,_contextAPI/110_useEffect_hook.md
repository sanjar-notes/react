# 110. useEffect hook
Created Tuesday 08 March 2022

#### What is an effect, aka "side effect"?
The main job of React is to:
1. Render UI
2. React to user input.

Tasks other than these 2 are "side effects". Example - http requests, computation, timers, using `localStorage`.

### Why
Side effects cannot be coded "as is" into the component function, because:
- They'll be implemented each time the component is rendered, i.e. function is executed. This may be very expensive, or not needed.
- If the side effects change state (using `useState`), then this will trigger an infinite loop. How: `side-effect` --> `change state` --> `re-render due to change state` --> `side-effect` 🔁 and so on.

So how do we code side effects into components, in a controllable way. The answer is the `useEffect` hook.

### How
Syntax of `useEffect`:
```jsx
import {useEffect} from 'react';

const MyComponent() {
	...
	useEffect( () => {...}, [...]);
	...
	return <>...</>;
}
```
It has two pieces:
1. Dependency array - just variables. React keeps track of these.
2. A function that runs *after* every render if any dependencies have changed. Side effect code goes into this function.

###### Note on dependency array
1. If dependency = `undefined`, i.e. absent. Function will run after every render.
2. If dependency = [] (empty array), the function will execute once, i.e. after first render.
3. If the dependency array has any candidates, the function will run after every render, given the dependencies have changed.

### What
- `useEffect` is the solution to the problem of placement (and therefore execution) of side-effect (s) code.
- `useEffect` is not like `useState`. i.e. it won't trigger re-render due dependency array change. It will do so only if state is changed inside the function, which is not the question here. Again, to reiterate - `useEffect` runs the function after every render if any dependency has changed.

###### When to use `useEffect`?
FIXME - can be made better
Use it when:
1. The task is a side-effect. Note that all possible side-effect code is a part of `useEffect`, i.e. `useEffect` is for side-effects, the converse may not be true.
2. It is computationally expensive and/or not needed on each render.
3. For http requests, DB/`localStorage` read/writes may use `useEffect`.
4. Try to avoid `useEffect` as much as possible - FIXME: Why, Really?
5. You'll know.