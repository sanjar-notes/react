# 5. Lifting state up
Created Friday 11 February 2022

## Why
Parent can communicate (i.e. send data) down to children using props.

But how do children communicate back to parents. Also, is this even needed ? Yes, it is needed. It's needed when:
1. Entered input needs to change state of the whole app (example: dark mode toggle button). So communication must happen from the input component to the display component, via a common ancestor.
2. NodeA to NodeB communication via lowest common ancestor.

## How
Solution: We can create function in a parent component that mutates state and pass it as prop to a child component. The child component will call the passed prop (a function) with an argument (the data to be communicated). This way, data is communicated upwards (child --> parents).

If there're multiple components between child and parent, each component can call its prop function and each component will receive a function as prop from above.
```jsx
import React, { useState } from "react";

import Child from "./Child";

function Parent() {
  const [vari, setVari] = useState("Ready to receive...");

  return (
    <div>
      {vari} <Child sendToParent={setVari} />
    </div>
  );
}

export default Parent;
```
```jsx
import React from "react";

function Child({ sendToParent }) {
  const clickHandler = () => {
    sendToParent(Math.floor(Math.random() * 100));
  };

  return <button onClick={clickHandler}>Send</button>;
}

export default Child;
```

## What
- It should be noted that we need "state" to pass data upwards (child --> parent). Can't be done without state. The reason is that the `setFunc` changes the state, which is a variable outside the flow of the component function. And also that the `setFunc` is exportable (of course it is, no big deal!).
- Also, the above point helps design a component, as it makes it imperative for stuff that's to be lifted up be a state variable, and not a usual variable.
  
## Conclusion
So basically, we're making state available to the parent via a function passed via prop.