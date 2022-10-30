# 297. Building the code for production
Created Sunday 30 October 2022

## Why
- We use `Node.js` as a runtime for our development, and libraries. These are not directly executable in a browser.
- Also, we don't use all parts of React or libraries we used to build our app. So it doesn't make sense to ship parts which are not needed.

So, we "build" the app code. This generates optimized client side code that can be placed on a server for consumption by browsers.

Note: 
- This "optimization" done on "build" is configured by default by React and libraries, and refers to bundle size optimization, not the performance of what the code does. Things like `useMemo`, `React.memo`, app architecture need to be done separately.
- The build step will automatically generate multiple `.js` and `.css` files for each of the lazy loaded entities.


## How
Not important now.


## What
To build a React app created with `create-react-app`, run `npm run build` from root the app folder. The generated files are kept in `/build` folder. It's not best not to edit them, at all.

Of course, one can edit things like index.html, favicon, robots.txt in the `public` folder before building the code.

Contents of `/build` folder are kept on the server, as is.