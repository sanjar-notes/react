# 203. Handling the "was untouched" state
Created Monday 25 July 2022

- We used a trick [here](https://github.com/exemplar-codes/reactjs-forms-user-input/commit/b83389e620ea8307103053b1bdf65053e86adca1) - we set the form as *valid* when it loaded. This may become a problem, for example, if were using `useEffect` to do some a request if the form is valid.
- This trick may be harmless in many scenarios, but it is semantically wrong part of our app.
- The problem can be solved by having another state, which just stores the fact that the form is untouched or not. We can set the form to be invalid initially and use this new state to not run requests. This would be semantically correct code.