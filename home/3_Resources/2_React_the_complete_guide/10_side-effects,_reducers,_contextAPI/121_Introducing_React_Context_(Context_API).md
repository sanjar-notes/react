# 121. Introducing React Context (Context_API)
Created Tuesday 14 March 2022
- [ ] in vault

### Why
##### Situation
We pass data:
1. Down (parent --> child) using props.
2. Up (child --> parent) by lifting state up.

But many times, it happens that the source and destination are not directly connected.
In this case, we pass props or lift state up through components that don't have anything to do with the data being passed i.e. they are just used as "plumbing" for passing data.

This is fine from a functionality point of view.

##### Problem
But this is not good from a code-design point of view, because only relevant data should remain at relevant places. Data not related to a component should not at all be handled to it, i.e. for "plumbing" purposes.

Even if the code-design is ignored, for bigger apps, this leads to bad code, because it becomes difficult to know which component is actually using the data and which component is just used for forwarding data.

FIXME: Is it really a problem though, we could have just marked props as "forwarding"/"relevant".

##### Solution
Have a "component-wide" (component wide global) state storage, which is read/written to by the relevant components.
This makes the code more elegant.

FIXME: is using a relatively "global" state a good thing?

### What
It's like a syntax sugar, where props are being handled in a marked way, i.e. plumbing props vs useful props. This is the implementation, I guess (FIXME: guess?).