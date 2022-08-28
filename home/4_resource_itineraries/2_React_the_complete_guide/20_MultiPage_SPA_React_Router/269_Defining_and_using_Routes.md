# 269. Defining and using Routes
Created Saturday 27 August 2022

The most basic way to have client side routing is to use `Route` to conditionally render components based on the current URL. The process is simple:
1. Nest the component you wish to render conditionally, given a URL, inside the `Route` component provided by React Router.
2. Then, nest the "root routing component"  of the app by `BrowserRouter`. This is usually the same as the root component of the app.
Done.
See [code](https://github.com/exemplar-codes/react-router-demo/commit/c32a78bf71ea31c68e60e4c06d5b1888d75674f3).