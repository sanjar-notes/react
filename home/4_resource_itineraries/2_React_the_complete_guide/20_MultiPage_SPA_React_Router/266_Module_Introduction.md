# 266. Module Introduction
Created Saturday 27 August 2022

- All projects I've made until now changes views but the URL always stays the same.
- Not having a URL is a big disadvantage. Having URLs lets the user share a link to specific parts of our application, which is a great feature of the web, in general.

- Now, we are building SPAs (single-page-application), meaning the page never refreshes. How do we implement URLs into an SPA?
- Well, we do something called client-side-routing. Meaning our SPA shell's JavaScript is such that it detects the current URL and switches to the appropriate view. Also, it can change the view and the URL based on user action (like clicking a button). This _simulates_ the behavior that URL and view are synchronous, as if a server is involved for page load (it isn't in reality).
- So, client-side-routing is actually an "illusion" of URL and corresponding view changes.

- We'll use an NPM package called `react-router` that helps us declaratively configure routing for a React SPA.
  
  In this module, we'll study about:
  1. Client Side Routing
  2. React-Router package