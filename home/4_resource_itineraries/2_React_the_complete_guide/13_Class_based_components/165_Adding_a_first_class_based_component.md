# 165. Adding a first class based component
Created Monday 14 July 2022

[Code link](https://github.com/exemplar-codes/react-with-classes)

This is a simple app written using functional component. And it uses a simple state.
Our goal is to rewrite it use Classes instead of function components.

---
Functional component:
```jsx
import classes from './User.module.css';

const User = (props) => {
  return <li className={classes.user}>{props.name}</li>;
};

export default User;
```
re-written as a class component:
```jsx
import { Component } from "react";
import classes from "./User.module.css";

class User extends Component {
  render() {
    return <li className={classes.user}>{this.props.name}</li>;
  }
}

export default User;
```
---
### Learnings
1. Class components need to extend from `React.Component`.
2. Class constructor is not needed for stateless components, in general.
3. Class needs to have a `render` method that returns JSX.
4. Props are accessed via the `this.props` variable. It is available by default, i.e. without a constructor.
5. Classes and functional components are interoperable, i.e. classes can use function components and vice-versa. One can mix and match whatever one prefers, but generally it's good to either use all functional or all class components. This may not be the case if the codebase is old, and contains class components, which is fine.