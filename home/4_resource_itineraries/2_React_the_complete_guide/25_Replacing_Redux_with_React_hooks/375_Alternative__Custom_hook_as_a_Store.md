# 375. Alternative: Custom hook as a store
Created Sunday 15 January 2023

Continuing with the [existing code](https://github.com/exemplar-codes/replacing-redux-with-context-and-hooks/tree/441b9578f944293c8adf11d4d508ca135a6a8d4a
).

## Alternative 2
We'll build a global state management solution without Redux or React-Redux or the Context API.

We'll only use custom hooks.

Code:
1. Creating the store solution - https://github.com/exemplar-codes/replacing-redux-with-context-and-hooks/commit/57b252df68cd147cddf235b0b8ef707aaeaa6680
2. Using it - https://github.com/exemplar-codes/replacing-redux-with-context-and-hooks/commit/c35c3400f69e5e50258e507bf173466f78f97c38

Explanation (this was really hard to wrap mind around, code wise, but the idea is simple).
1. We have 3 simple scoped variables in a file. We make changes to these variables. So they exist only once in the lifetime of our app. Reason: the variables are initialized only once, when something is imported from the file for the first time.
2. We manage all data in these three variables.
3. We expose a simple dispatch function that changes the global state, using the 'equals' sign. FIXME (why? BTW, doesn't work otherwise)
4. Optimize update to relevant parts - we create and store a so called _listener_ for each instance of the custom hook. When the global state is changed, we run this listeners, causing re-renders for all components that use the hook. Others component don't re-render, atleast not directly, as it should be.
5. Some more optimization, in usage code using `React.memo`. [Code](https://github.com/exemplar-codes/replacing-redux-with-context-and-hooks/commit/c1c0daf3d6f1738ff7ae55380a1eb711ee92f00b)
6. Remaining code is obvious.

## Lessons and observations
1. This is different from Redux, in that Redux has custom JavaScript only. Here, we stayed within the React ecosystem.
2. React hooks are a very powerful concept. When used properly, it feels like a custom version of React.
3. Using Redux is fine, but such a custom hook may be used if the goal is to minimize the bundle at a bytes level.


## Conclusion
This section was OK, but it was too hairy for a demo. I'll stop here, I'm confident I can code this up if the situation demands. Here's the [code - ZIP file](![](../../../../assets/replace-redux-06-bonus-multiple-slices.zip)) for multi-slice implementation of this demo project.

\_TAG_: skipped at the end, not the best use of my time + I'm late.