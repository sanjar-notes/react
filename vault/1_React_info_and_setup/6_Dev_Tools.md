# 6. Dev Tools
Created Mon Jan 8, 2024 at 9:16 PM

> Basically, we can complete view the tree, inspect it and also reach exact points in code. console.log for props is very inefficient.

## Chrome Dev tools
Used if other tools don't work.
For exact inspecting styling - Chrome dev tools inspect.

## React Developer Tools
A browser extension
React Developer tools are very good and absolutely needed for productivity.
https://react.dev/learn/react-developer-tools

They help:
1. Inspect component tree. Optionally, HTML nodes can be included into the tree.
2. See props and state
3. Identify performance problems

The main point here is that they make the app traversable via your components instead of just HTML (like browser dev tools).


## Redux DevTools
A browser extension
https://github.com/reduxjs/redux-devtools/

Mainly to
- Inspect slices
- Inspect actions
- Do time travel debugging of the store, actions


## LocatorJS
A browser extension
https://www.locatorjs.com/

 Use this extension to jump to code (in correct file, at correct line number) by selecting the UI (without opening dev tools) - activates via a shortcut.
 Takes you directly into the editor (vscode).
 
 Locator is non-myopic - if you hover just outside a component, it shows a different background, which prevents going into reusable component files. Awesome


For shallow inspect spaceing - 'Desisgner tools' plugin