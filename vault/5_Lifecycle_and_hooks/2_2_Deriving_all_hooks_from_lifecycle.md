# 2.2. Deriving all hooks from lifecycle
Created Tuesday 06 February 2022

### Why
It's simple to derive lifecycle methods after considering the lifecycle of a React component.

---
### How
There are 2 steps to derive/understand hooks:
1. Consider all possible hooks w.r.t lifecycle phases - places where state could be changed/set for rendering.
2. Remove duplicate and unneeded hooks.

After doing this, only 3 hooks remain, namely:
1. `componentDidMount`
2. `componentWillUnmount`
3. `componentDidUpdate`

All other hooks, as said, are either unnecessary (they do nothing) or duplicate (can be replaced by existing hook).

---
### What
Here's the lifecycle and hooks derivation, HD photo: [MEGA link](https://mega.nz/file/CNtjSI4b#rd33QDBvvW6t94r198WxgFy7cZp5T4Z67m-7of0RpqY)
The result is [this](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/).