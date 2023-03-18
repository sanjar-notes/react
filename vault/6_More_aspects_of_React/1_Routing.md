# 1. Routing
Created Monday 30 May 2022

FIXME:
1. What is routing in SPA? 
2. Why do we need it? Maybe this will help: https://stackoverflow.com/q/39636411/11392807
3. What is react-router library
4. How to code it
---
4. Add this info if needed
React Router refers to the standard library used for routing in React. It permits us for building a single-page web application in React with navigation without even refreshing the page when the user navigates. It also allows to change the browser URL and will keep the user interface in sync with the URL. React Router will make use of the component structure for calling the components, using which appropriate information can be shown. Since React is a component-based framework, it’s not necessary to include and use this package. Any other compatible routing library would also work with React.

The major components of React Router are given below:
- **BrowserRouter**: It is a router implementation that will make use of the HTML5 history API (pushState, popstate, and event replaceState) for keeping your UI to be in sync with the URL. It is the parent component useful in storing all other components.
- **Routes**: It is a newer component that has been introduced in the React v6 and an upgrade of the component.
- **Route**: It is considered to be a conditionally shown component and some UI will be rendered by this whenever there is a match between its path and the current URL.
- **Link**: It is useful in creating links to various routes and implementing navigation all over the application. It works similarly to the anchor tag in HTML.
---
5. Read and explain from: https://dilshankelsen.com/an-introduction-to-react-router/ and https://reactrouter.com/