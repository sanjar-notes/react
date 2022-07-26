# 191. A more realistic example of custom hook
Created Tuesday 24 July 2022

We'll look at some complications and their solutions, that can arise in a real use case.
Consider [App.jsx](https://github.com/exemplar-codes/react-custom-hooks-realistic-example/blob/cbfbbc15df2b8069460d807868fd37e2f187df7f/src/App.jsx) and [NewTask.jsx](https://github.com/exemplar-codes/react-custom-hooks-realistic-example/blob/cbfbbc15df2b8069460d807868fd37e2f187df7f/src/components/NewTask/NewTask.jsx). Observe that:
1. Both make HTTP requests, method varies of course.
2. Both do some work on the JSON data response.
3. Both handle `isLoading` and `error` states.
4. Both create and call a function encapsulating `fetch` either as a callback or in `useEffect`, so we'll do the same, i.e. return a callback.

- We can extract this functionality out to a custom hook.
- There are two possible ways to do this - pass the `onSuccess` functionality, `url`, `method` and `payloadBody` to the hook, or let them be parameters of the callback being returned by the hook.
- We'll choose the latter, because we need to work with `taskText` as input in `NewTask.jsx.
- We should return the callback by wrapping it inside `useCallback`, and as it doesn't take any external variables (parameters are internal variables), we don't need to provide a dependencies list.
	Had we chosen to provide the arguments to be passed to the hook, we'd have to use `useCallback` and also mandate that the `onSuccess` being returned be wrapped inside `useCallback` as well, which would hurt the hook's usability.

See final result, [here](https://github.com/exemplar-codes/react-custom-hooks-realistic-example/commit/ffa88863002e66bc86a9222c35c2ad8bd65a1812).

---
Custom hooks behave very fluidly and don't require any special syntax. But they can sometimes become convoluted if the custom hooks behavior needs to be heavily varied (as that will increase parameters in the hook and therefore complexity).