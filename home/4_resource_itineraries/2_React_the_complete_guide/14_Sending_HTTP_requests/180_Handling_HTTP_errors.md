# 180. Handling HTTP errors
Created Monday 19 July 2022

### Why
We should show errors if they error, in the UI.


### How
- Have an "error" state and a conditionally rendered component with a message/animation indicating an error has occurred.

An important observation: HTTP request errors don't trigger an error (similar to `throw Error`) when using `fetch`. The browser simply prints a message in the console and moves on.
To detect HTTP errors, check `fetch` `response`'s `ok` attribute. If that is true, everything is OK, else something has went wrong. So `throw` an error conditionally, and catch it in the `.catch` (if using promises) or `catch` clause(if using `async/await`). Also, update the error state in this clause, which will cause a re-render.

- The axios library does trigger a JS error.
- Error are handled in different ways by different APIs - some return an error response, other return a JSON with some message. Error handling, thus, depends on the API being consumed.
  
  
### What
Handled similar to loading state.