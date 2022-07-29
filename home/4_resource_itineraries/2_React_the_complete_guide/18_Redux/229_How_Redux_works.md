# 229. How Redux works
Created Thursday 28 July 2022

##### Redux's working architecture
- One data (state) store for the entire application, which stores all cross-component and app-wide state.
- Components set up "Subscriptions" to the store, for relevant data. These subscriptions trigger component re-render when the relevant data changes in the store.
- Store mutation is triggered when a component "dispatches" an "action", which calls a "reducer". This *reducer* mutates the store.
- The components which subscribed to the relevant store data (which changed), get re-rendered.
The process continues 🔄.
  ![](../../../../assets/Pasted%20image%2020220728123846.png)