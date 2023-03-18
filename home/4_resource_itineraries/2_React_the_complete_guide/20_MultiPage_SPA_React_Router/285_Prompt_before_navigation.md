# 285. Prompt before navigation
Created Monday 26 September 2022

## Situation
Show a prompt, triggered on navigation. 

e.g. when the user tries to navigate away (using forward/backward buttons or otherwise) from an unfinished form.

## Why
-

## How
React Router may be using an "onURLChange" event listener.


## What
React Router provides the `Prompt` component for showing a prompt.
The component takes two props:
1. `when` - a boolean. If true, then a "prompt" is shown on navigation.
2. `message` - a function that must return a `string`. This string will be shown on the prompt. Additionally, the function gives access to a "location" as the param, of course.

Example:
```jsx
function App() {
  return (
    <>
      <Prompt when={true} message={() => "Leave the page?"} />
      <Link to="/welcome">Navigate</Link>
    </>
  );
}
```

See more [examples](https://github.com/exemplar-codes/react-router-demo/tree/prompt_component).