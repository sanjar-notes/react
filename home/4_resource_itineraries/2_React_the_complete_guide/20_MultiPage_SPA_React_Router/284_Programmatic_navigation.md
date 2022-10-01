# 284. Programmatic navigation
Created Sunday 25 September 2022

Also known as imperative navigation.

# Why
Navigate when a button is clicked. Or more generally, navigate programmatically.


## How
Simple, use the native History API.
But it'll be helpful if React Router instance knows about such navigation.
Optionally, save/load/retain some state and run a callback function.


## What
- React Router has a `useHistory` hook that returns a 'History' object that's in sync with the router.
- The history object has many useful functions, such as:
	1. `push(newPath)` - navigates page and pushes the new path as browser history, allowing for the navigation buttons (forward/back) to work. Note: `push` has nothing to do with appending to nested routes.
	2. `replace(newPath)` - navigates page but doesn't make any changes to the history.
	3. `goForward()` - programmatically activate the forward navigation button.
	4. `goBack` - programmatically activate the back navigation button.

Example:
```jsx
import { useHistory } from 'react-router-dom';

function App() {
  const history = useHistory();
  
  const onClickHandler = () => history.push("/welcome/bingo");
  
  return (
    <button onClick={onClickHandler}>Click me</button>
  );
}
```

## Note
The page re-renders on navigation, always. Even if the new URL is the same as the current one, or we use `history.replace()`.