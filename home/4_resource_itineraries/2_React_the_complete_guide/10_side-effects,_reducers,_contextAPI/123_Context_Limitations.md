# 123. Context Limitations
Created Tuesday 06 May 2022
- [ ] in vault


###### What are the limitations?
1. This is not a limitation, but just a reminder - context is for managing state and props are for configuring (i.e. passing arguments) to reusable components. So context API cannot and should not be used everywhere. Props are still vital and have a separate role.
2. React context is not optimized for frequent state changes. This is just how it is designed. The tool that allows for both global state and fast changes is Redux.js, which we will learn soon.
3. Components subscribed to context (i.e. have `useContext`) in them will be updated, even if part of context they're using is unchanged. i.e. re-renders aren't as granular as they could be. *Redux* doesn't have this issue, since one can "subscribe" to specific parts of the store too, and the component gets a re-render signal only when those parts change.