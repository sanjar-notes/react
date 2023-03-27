# 229. How Redux works
Created Thursday 28 July 2022

##### Redux's working architecture
- One data (state) store for the entire application, which stores all cross-component and app-wide state.
- "Subscription" callbacks can be set-up with the store. These subscriptions trigger the callback when the store changes.
- Store mutation is triggered when by running the "dispatch" function and passing an "action", which calls a "reducer". This *reducer* mutates the store.
The process continues 🔄.

As evident, Redux has nothing to do with React. It's a standalone library.

For React apps, we can subscribe in such a way that component relevant store changes causes re-render of the component.
![](assets/229_How_Redux_works-image-1.png)
