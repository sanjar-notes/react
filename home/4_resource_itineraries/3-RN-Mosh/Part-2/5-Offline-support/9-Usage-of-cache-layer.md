# 9. Usage of cache layer
Created Sat Dec 30, 2023 at 1:55 PM

Since we don't know when a network outage may happen, we need to cache periodically, or maybe even with each important API call.

In an app, we usually have the following structure.
component <--> context/store <--> axios/networking-lib

Now adding the cache code in components or even in the context/store is pretty low level and shouldn't be a concern when developing a feature. And since its related to networking, caching code should be kept close to networking code, and as far away from app/feat code as possible.

## Where to add code in API lib
Assume we're using axios for networking. Now axios code isn't large but it's frequently changed and needs to be correct, so doing caching by hand near networking isn't good.

It should happen "automatically" and be "invisible". The simplest way is to just override the API library core function(s), and run your caching code beside them. This way, none of the components, store or API code changes, and we only made a one line change at one place.

This makes sense too, since if network is down, and during a fetch, we give back cached data, the flow remains the same, it's as if the data really came from the server.

*Intuitively, keep "habits" (frequent needs) of the app at a low level, away from app code as much as possible*.

## Code
```jsx
axiosClient.get = (...x) => {
  // before caching code
  const ret = await axiosClient.get(...x);

  // cache code here
  
  return ret;
}
```

## Clarifications
- Remember, "caching" is about "reads"
- Actions are hard to account for in a bad connection. And its sometimes impossible, since frontend part of an app only does a small number of validations, and the backend may run more, or may have external dependencies for validations. Example: is username taken?