# 372: Alternative: Using the Context API
Created Saturday 14 January 2023

## Approach 1
Let's start with approach \#1. For this we'll use the Context API.
Let's add the code. Here's the [change](https://github.com/exemplar-codes/replacing-redux-with-context-and-hooks/tree/441b9578f944293c8adf11d4d508ca135a6a8d4a
).

This *replacement* was easy.

What's the issue with this approach.
1. **Bad performance** - [Technically](https://github.com/facebook/react/issues/14110#issuecomment-448074060), the Context API is meant (FIXME: source?) for low-frequency and "mostly global" updates. In our demo project, switching favorites is a high-frequency update. Examples of low-frequency changes - theme, settings. The reason for this is that the Context API is neither optimized nor meant to observe nested changes in it's state. Consequently, it will re-render every component, even if the change was a nested one affecting only one component, which may lead to bad performance. **So**, use the Context API if state changes of an app are low-frequency, "most global" or if the app is small in size.
2. **Un-opinionated nature** - Redux being opinionated is good for very large apps/stores which may have their middlewares (or some other construct like that). Of course, stuff like reducers and action become more important for maintaining a consistent structure to interact with the store.
3. **Dev tool for debugging** - as of now, Redux allows time-travel debugging and a nice UI for it. No such tools exist for the Context API, as far as I know.
   
   BUT, there's still, a non-Redux alternative for global state management. 