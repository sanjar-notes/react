# 3. Section 7 - Debugging React apps
Created Wednesday 16 February 2022

Doing this now.

### 3. Kinds of errors in React
1. `npm start` does detect and show compilation errors in React projects. This is quite useful.
2. Warnings and prop errors are not compilation errors, so they are shown in the `console` tab in devTool.
3. Then there are logic errors like using bad `key` attribute for a list of components, which can make the order wrong.

### 4. Working with the debugger in DevTools
- When working with `create-react-app` created project and using `npm start`, JSX (or JS) files are available as is in the `Sources` tab in the DevTool. These files are of course not run by the browser, but they are in sync with the files being compiled and executed. So if a breakpoint is added somewhere in the React (JSX or JS) file, it will be a valid breakpoint.
- This source <--> compiled files fast bridge is an awesome thing that should be used to the fullest.

### 5. Using the React devTool
This a browser extension called `React Developer Tools`. They are available in both Chrome and Firefox, although Chrome is recommended.
- Once the extension is installed. Two tabs called `Components` and `Profiles` are made available in the devTool tabs besides Console, Sources, Network etc.
- `Components` shows the component tree of the app. It also has a cursor to locate React components directly by pointing to the UI.
- We can also see/edit the following stuff for various components in the `Components` tab:
	- children
	- parents (dependent)
	- props
	- source code line.
	- hooks (aka lifecycle methods)
This is very useful to understand and locate components of an app, especially if it's not written by me.
