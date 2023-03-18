# 271. Using NavLinks
Created Sunday 28 August 2022

### Why
Consider this [code](https://github.com/exemplar-codes/react-router-demo/commit/28ac9b51da8d683876eca2e41d0a6bd2ef826621). There's an important feature that's missing - we should be able to somehow highlight on what page we are (by highlighting the link). This, if done, normally, will take some custom code, i.e. something like `className={window.location.pathname === '.../path' ? {styles_for_navLink}: {}}`.

React Router provides a functionality to *add* CSS classes to `Link`s based on the current URL. Instead of `Link` (which is agnostic to current URL), use `NavLink`, which accepts a class as prop that gets applied conditionally based on current URL.

### How
Syntax:
```jsx
{// 1. Simple class
<NavLink activeClassName='myActiveClass' to="/welcome">Welcome<NavLink>

{// 2. CSS modules
import classes from './MyComponent.module.css';

<NavLink activeClassName={classes.myActiveClass} to="/welcome">Welcome<NavLink>;

{// 3. If activeClassName prop is omitted
<NavLink to="/welcome">Welcome</NavLink>;
 
{/* added class name will only be present if current URL matches 'to' prop value */}
```
will render as:
```html
<a href="/welcome" class="myActiveClass">... <!-- URL === '/welcome', prop used - string or CSS module - #1, #2 --> 

<a href="/welcome" class="active">... <!-- URL === '/welcome', prop not used, #3 -->

<a href="/welcome" >... <!-- URL !== '/welcome', no class by Router -->
```
Note:
1. If `activeClassName` prop is omitted, 'active' is added as class, otherwise prop value is added as class, assuming URL match.
2. If current URL does not match, no classes are added by React Router.


### What
`NavLink` behaves just like `Link` except conditional classes based on current URL.

See [code example](https://github.com/exemplar-codes/react-router-demo/commit/4cbb0b0fad4bab9c6451b254b15fd81ec953b490).