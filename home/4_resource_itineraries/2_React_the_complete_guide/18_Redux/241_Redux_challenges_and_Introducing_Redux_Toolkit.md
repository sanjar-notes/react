# 241. Redux challenges and Introducing Redux Toolkit
Created Saturday 30 July 2022

There's an easier way to use Redux in React projects.
List of potential problems with existing way of using Redux(i.e. `redux` + `react-redux`) for large apps:
1. Clashing action terms.
2. Long reducer function due to absence of state merging.
3. State immutability rule could be ignored.

- Redux Toolkit solves these problems and makes working with Redux with React easier.
- Redux Toolkit is created by the same team as `redux` and `react-redux`.
- Redux Toolkit is also known as RTK.

### Why Redux Toolkit?
FIXME(reasons - to make the reducer and store maintainable by chunking it into multiple reducers and "slices")