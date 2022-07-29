# 230.1. Core Redux with React
Created Friday 29 July 2022

[Code](https://github.com/exemplar-codes/core-redux-react-demo)

What I did here:
1. Used `React.useState` for re-rendering the component and triggered it in the reducer. See [code](https://github.com/exemplar-codes/core-redux-react-demo/commit/260bdf1a94cc108b35cc7f52cd74a8dca8a9f8f2).
2. Used a hook to do the same. See [code](https://github.com/exemplar-codes/core-redux-react-demo/commit/8b991bb392e292a17dce6b9c7b3aa4bfc843b33e).

Shortcomings and solutions:
1. How to re-render multiple dependent components when the store is changed by any component? One way is to store the re-render function of the root of this cross-component store, and re-evaluate that, causing a re-render of all the dependent components. This can be done by exporting a custom dispatch function from the root of the cross-component section, which also calls re-render. This exported dispatch may called by descendants, and will re-render the whole cross-component section. *In short, we need to "Provide" as in `useContext`*. See [code](https://github.com/exemplar-codes/core-redux-react-demo/commit/753de6d926b30f674dfc593388e5e1ee3ae38b63#diff-26da19e39a61206e097a8088a139c7ccfc4ac5c4139a5d581bda5e55976ab538).