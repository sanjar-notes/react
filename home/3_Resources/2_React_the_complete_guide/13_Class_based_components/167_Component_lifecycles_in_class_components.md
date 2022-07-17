# 167. Component life-cycles in class components
Created Monday 15 July 2022

Class based components can't use React hooks. So how do we run side-effects?

Class based components have a somewhat imperative API for running side-effects, which exposes the life-cycle methods directly.

The most common life-cycle methods are:
1. `componentDidMount` - called after the component first mount (i.e. evaluation and render are complete) to the DOM. Equivalent to `useEffect(..., [])`.
2. `componentDidUpdate` - called after the component has updated (i.e. evaluation and *potential* render are complete) to the DOM. Equivalent to `useEffect(...)`. If one uses `if` conditions inside this function, it'll become equivalent to `useEffect(..., [someValue])`.
3. `componentWillUnmount` - called just before the component is unmounted from the DOM. Equivalent to the cleanup function of `useEffect`.
   
Transform functional component that uses `useEffect`:
```jsx
import { useState, useEffect } from "react";
import classes from "./UserFinder.module.css";
import Users from "./Users";

const DUMMY_USERS = [
  { id: "u1", name: "Max" },
  { id: "u2", name: "Manuel" },
  { id: "u3", name: "Julie" },
];

const UserFinder = () => {
  const [filteredUsers, setFilteredUsers] = useState(DUMMY_USERS);
  const [searchTerm, setSearchTerm] = useState("");

  useEffect(() => {
    setFilteredUsers(
      DUMMY_USERS.filter((user) =>
        user.name.toLowerCase().includes(searchTerm.trim().toLowerCase())
      )
    );
  }, [searchTerm]);

  const searchChangeHandler = (event) => {
    setSearchTerm(event.target.value);
  };

  return (
    <div className={classes["finder"]}>
      <input type="search" onChange={searchChangeHandler} />
      <Users users={filteredUsers} />
    </div>
  );
};

export default UserFinder;
```
to class based component:
```jsx
import { Component } from 'react';

class UserFinder extends Component {
  constructor() {
    super();
    this.state = { filteredUsers: DUMMY_USERS, searchTerm: "" };
  }

  searchChangeHandler(event) {
    this.setState({ searchTerm: event.target.value });
  }

  /*
  useEffect(() => {
	setFilteredUsers(
	  DUMMY_USERS.filter((user) =>
		user.name.toLowerCase().includes(searchTerm.trim().toLowerCase())
	  )
	);
  }, [searchTerm]);
  */
  
  componentDidUpdate(prevProps, prevState) {
    if (prevState.searchTerm !== this.state.searchTerm) {
      // update list
      this.setState({
        filteredUsers: DUMMY_USERS.filter((user) =>
          user.name
            .toLowerCase()
            .includes(this.state.searchTerm.trim().toLowerCase())
        ),
      });
    }
  }

  render() {
    return (
      <div className={classes["finder"]}>
        <input type="search" onChange={this.searchChangeHandler.bind(this)} />
        <p>{this.state.searchTerm}</p>
        <Users users={this.state.filteredUsers} />
      </div>
    );
  }
}

export default UserFinder;
```

### Learnings
1. `componentDidUpdate` receives two parameters - previous props and previous state. These may be compared with the new props or state, in order to avoid infinite loops.
   ```jsx
   componentDidUpdate(prevProps, prevState) {
	   if(prevState.x != this.state.x) {
		   // do something
	   }
   }
	```
2. Using life-cycle methods in classes is a different mental model. It is more imperative, and less concise than `useEffect` in functional components.


### An important observation - re-instantiation of components is avoided, unless absolutely needed
The `componentDidUpdate` function receives previous props, in addition to previous state.
Having previous state was fine, but why does it receive previous props? Well the answer to this question is that when comparing (during tree diffing) two *custom* components of the same type, even if there are changes in props, the instance of the component remains the same (this is actually the reason state is preserved between renders), irrespective of prop changes. Of course React runs the `render` method and then diffs it with the existing tree.

In short, the important thing to note here is that components are instantiated only once, even between multiple renders, including if the re-render call came from the ancestor i.e. re-evaluation is related to `render` output instead of `constructor`.

Source: https://reactjs.org/docs/reconciliation.html#component-elements-of-the-same-type

FIXME: get a little more comfortable with how this works. I'm a little foggy with this, but it doesn't matter, this is a nuanced implementation detail.