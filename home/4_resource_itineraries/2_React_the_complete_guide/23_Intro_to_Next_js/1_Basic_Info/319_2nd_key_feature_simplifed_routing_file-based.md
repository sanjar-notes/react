# 319. 2nd key feature: simplified routing - file-based
Created Tuesday 6 December 2022

## Situation
In a simple HTML, CSS and JS website. We create pages whose name is the same as the request route, which are sent to the client when we receive a request for the route. Simple.


## Why
idk, it's intuitive perhaps.


## How
Next.js, does the same, on the first request. For this, the framework has a file-based routing mechanism, i.e. we create pages whose name matches the routes a user can request.

When the first request is received, the SSR process (which runs on the backend) locates the page from the request route and pre-renders it with the relevant data, before sending it.

After the initial load on the client, the app follows a standard client-side routing approach.


## What
All pages, in Next.js, are kept in the `pages` folder. The name of the file in `pages` indicate the route it'll be pre-rendered for.

To specify nested routes, we basically make a folder, with the children pages (routes) being files or folders (for more nesting, if needed).

![](assets/319_2nd_key_feature_simplifed_routing_file-based-image-1.png)

**Opinion**: The whole SSR experience can be optimized, maybe in some cases, if we do code-splitting along with SSR, which can be used to reduce bundle size.
