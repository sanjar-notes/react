# 270. Working with Links
Created Sunday 28 August 2022

- We used `Route` to conditionally render components based on a URL. But what about hyperlinks, what happens when we click one? 
- Does it override browser default of making a request and change the URL? Well, no[(see code)](https://github.com/exemplar-codes/react-router-demo/commit/a2c7b4830dcd4126fbcd4dc98046605c7bae00a4). The `a` tag is impervious to effects from the React Router, this is by design because even in an SPA, we may have links to external resources. So `a` tags will cause a reload (which we wish to avoid for in-app links).

Instead of `a` tags, use the `Link` component provided React Router,  for internal links (i.e. within the app). The `Link` component, on click:
1. Changes the URL
2. Prevents requests on URL change
3. Re-renders the app, so that `Route`s are evaluated according to the new URL.