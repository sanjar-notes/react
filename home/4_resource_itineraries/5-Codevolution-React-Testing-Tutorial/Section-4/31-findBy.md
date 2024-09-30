# 31. findBy
Created Mon Sep 30, 2024 at 1:19 PM

## Why
`get` and `query` are sync methods, they assume the UI has been rendered. i.e. they dont wait.

But web apps are all about async calls, so the UI may not have loaded.
i.e. we also need to handle
- Apperance/disapperance of elements
- Async renders, i.e. renders after some time.

## `findBy` and `findAllBy`
- Returns a promise which resolves when an element is found
- The promise is rejected if the query fails (as per find vs findAll) with a default timeout of 1000ms.

```jsx
const myButton = await screen.findByRole("button", {name: "button" }); // suppose this appears after 500ms
expect(myButton).toBeInTheDocument(); // will pass


const myButton = await screen.findByRole("button", { name: "button" }, { timeout: 2000 }); // set custom timeout in 3rd arg
``` 