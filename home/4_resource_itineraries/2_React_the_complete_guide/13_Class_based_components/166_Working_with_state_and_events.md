# 166. Working with state and events
Created Monday 15 July 2022

Goal: convert a functional stateful component from class based one.

Functional code:
```jsx
import { useState } from 'react';
import User from './User';

import classes from './Users.module.css';

const DUMMY_USERS = [
  { id: 'u1', name: 'Max' },
  { id: 'u2', name: 'Manuel' },
  { id: 'u3', name: 'Julie' },
];

const Users = () => {
  const [showUsers, setShowUsers] = useState(true);

  const toggleUsersHandler = () => {
    setShowUsers((curState) => !curState);
  };

  const usersList = (
    <ul>
      {DUMMY_USERS.map((user) => (
        <User key={user.id} name={user.name} />
      ))}
    </ul>
  );

  return (
    <div className={classes.users}>
      <button onClick={toggleUsersHandler}>
        {showUsers ? 'Hide' : 'Show'} Users
      </button>
      {showUsers && usersList}
    </div>
  );
};

export default Users;
```
re-written as a class component:
```jsx
import { Component } from "react";

class Users extends Component {
  constructor() {
    super();
    //   const [showUsers, setShowUsers] = useState(true);
    this.state = { showUsers: true };
  }
  toggleUsersHandler() {
    // setShowUsers((curState) => !curState);
    this.setState((latestState) => {
      return { showUsers: !latestState.showUsers };
    });
  }

  render() {
  // stateless helper functions/datum are OK inside render()
    const usersList = (
      <ul>
        {DUMMY_USERS.map((user) => (
          <User key={user.id} name={user.name} />
        ))}
      </ul>
    );

    return (
      <div className={classes.users}>
        {/* <button onClick={toggleUsersHandler}> */}
        <button onClick={this.toggleUsersHandler.bind(this)}>
          {this.state.showUsers ? "Hide" : "Show"} Users
        </button>
        {this.props.children}
        {this.state.showUsers && usersList}
      </div>
    );
  }
}

export default Users;
```

### Learnings
1. **Callbacks** should usually be made instance methods.
   - The proper way to specify an instance callback function is like this - `this.myFunction.bind(this)`. e.g. `<button onClick={this.myFunc().bind(this)}>`.
   - Calling it does not require `bind`, i.e. `this.myFunction()` is OK.
   - We can still have helper functions/data in the render if we like, but callbacks involving state are better kept out of the `render` method.
2. Working with **state**:
	1. Initialization - initialize an instance variable called "state", which must be an `object`. With class based components, all state variables are always kept in this object called "state".
	2. Updation - to update state, use the React provided instance method called `setState` which has two versions, just like the mutator provided by `useState` hook:
		1. Pass the new state *changes*, as an object.
		2. Pass a function that provides the latest state and returns the new state changes. This is used if the new state depends on the previous state.
		   
		Note: `setState` automatically merges changes - we only pass the *changes* to be made as an object, and React will automatically *merge* the new state object with the existing state. i.e. the state is merged, not overridden. This is different from `useState`, where state is overridden, instead of being merged.
		Example of state change:
		```jsx
		class MyComponent extends Component {
			constructor() {
				super();
				this.state = {odd: false, color: 'blue'};
			}
	
			toggleParity() {
				this.setState(prevState => {parity: !prevState.parity});
			}
			
			render() { return <>...</>; }
		}
		```
3. Imported classes work exactly the same as functional components.