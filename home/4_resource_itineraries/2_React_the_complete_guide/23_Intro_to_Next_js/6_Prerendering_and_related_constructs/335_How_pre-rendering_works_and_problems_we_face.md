# 335. How pre-rendering works and problems we face
Created Saturday 17 December 2022

- Pre-rendering in the context of SPAs means that we ship atleast some markup in our UI response.
- This is the most popular reason for using Next.js

Pre-rendering is not an absolute term, and lies on a spectrum. 3 levels of it are:
1. No pre-rendering - empty SPA shell, completely hyrdated on the client side. Example - plain React app.
2. Some pre-rendering - some parts are present in the UI, others are hydrated on the client side. Next.js apps
3. Full pre-rendering - all (as much as possible) parts of the requested page are already there in markup.

> **Next.js allows us to do all 3, but the default behavior is \#3 (full pre-rendering).**

It is important to note that choosing a pre-rendering level depends on the web page, audience, data velocity etc.

Next.js provides us with 3 constructs, which may be used to change the level of pre-rendering and the time (build time or request time) it is carried out, for a *given page*.

1. SSG - Static Site Generation - build page at "build time".
2. SSR - Server Side Rendering - build page at every request.
3. ISR - Incremental Server Rendering - build the page every 't' seconds, or some other criteria.

## SSG (Static Site Generation)
This is a pre-rendering mechanism, where the server *tries* to build the page at "build time".

In Next.js, the `getStaticProps` function is used for SSG. 

It is a function that runs at build time (so, on the server - things like filesystem, databases are all available) and returns some "props" that become available to the page component. Thus, files are generated and can be used as server responses.

It is only available for pages. To use it export (normal not `default`) a function named `getStaticProps` in the page file.

Note that using SSG (or `getStaticProps`) doesn't mean one *has to* hydrate the whole page on build time. For example, if you have a fetch (or `useEffect`) request inside the component, it will be ignored by Next.js (since it pre-renders the first snapshot returned by the page component), but will still run on the client. Of course, this also means that the resulting changes won't be there in the pre-rendered UI, which is may or may not be OK.

## SSR (Server Side Rendering)
This is a pre-rendering mechanism, where the server *tries* to build the page at every request.

**This is the "default" in Next.js**. One doesn't need to actually specify/code anything to enable this, the page component is enough. However, if one needs to run some server side code (for authentication, DB lookup etc), there is a way to do it - the `getServerSideProps` function.

It behaves similar to `getStaticProps`, but runs for every request. Additionally, it also receives the request and response objects as its parameters, and so can be used for authentication, responding with a status code etc.

It is only available for pages. To use it export a function named `getServerSideProps` in the page file.

SSR, like SSG, also doesn't mean all data has to there that the page uses, i.e. the page could hydrate parts of it on the client.

## ISR
Will study later.


## Important thing about pre-rendering in Next.js
Next.js pre-renders only the first snapshot of the page component. This means that `useEffect` and other stuff will be completely ignored by Next.js. `getStaticProps` or`getServerSideProps` will work as usual, since they are run before the component is executed for pre-rendering.

This is safe though, from a functionality point of view, since Next.js will still properly include and bundle `useEffect` and other logic that it ignores in pre-rendering.


## Pre-rendering in Next.js, in a nutshell
- **Page-wise mechanism** - SSG/SSR/ISR is decided for each page (by marked by existence of `getStaticProps`/`getServerSideProp`, and is therefore not a global setting (i.e. for all pages).
- **Default behavior** - Again, re-emphasizing that Next.js's default behavior is pre-rendering on every request, even if there's no `getServerSideProps` for the page.
- **First snapshot only** - Only the first snapshot of the page component is considered for pre-rendering. So things like `useEffect` are ignored for pre-rendering. They are still included in the the bundle though.