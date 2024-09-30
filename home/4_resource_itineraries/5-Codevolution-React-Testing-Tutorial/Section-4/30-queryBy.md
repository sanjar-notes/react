# 30. queryBy
Created Mon Sep 30, 2024 at 1:15 PM

`get` queries throw error if the element is not found. `query` methods just return a `null`.

So `query` methods are helpful for checkin absence.
```jsx
const myButton = screen.queryByRole();
expect(myButton).not.toBeInTheDocument();
```

Note:
- get vs getAll and query and queryAll behave in corresponding ways, i.e. throw error and return null.