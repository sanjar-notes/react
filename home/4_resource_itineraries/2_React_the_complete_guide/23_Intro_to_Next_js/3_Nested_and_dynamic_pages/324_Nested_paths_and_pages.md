# 324. Nested paths and pages
Created Wednesday 7 December 2022

## Nesting paths syntax
Examples (request route <=> file in `pages/`):
1. `/` <=> `index.js`
2. `/hello` <=> `hello.js`
3. `/hello` <=> `hello/index.js`
4. `/hello/en` <=>`hello/en.js`

\#2 and \#3 are almost equivalent ways to do the same thing. But \#3 is the approach used by Next.js for nested routes.

In other words, folders aren't pages, but they are used to specify nesting, with the `folderName/index.js` file mapping to `/folderName`.


## Page components
- All (`.js*`) files inside `pages` are pages.
- Every page is simply a React component. So no special changes in the code.
- The only requirement is that we need to `default` export the page component.
- Also, name of the component doesn't have to be same as the file name. It can be any valid React component name.

### Examples
`pages/index.js`
```jsx
// our-domain.com

function HomePage() {
	return <h1>Home page</h1>;
}

export default HomePage;
```

`pages/new.js`
```jsx
// our-domain.com/news

function AllNewsPage() {
	return <h1>News page</h1>;
}

export default AllNewsPage;
```

`pages/help/en.js`
```jsx
// our-domain.com/help/en

function HelpPageEnglish() {
	return <h1>Help page page</h1>;
}

export default HelpPageEnglish;
```

Note: we don't need to export `React`, Next.js has it autoloaded, which is how most React app projects are configured.


## Starting the dev server
Run `npm run dev` and go to `localhost:3000` (most probably) to see the web app.

[Nested routes code](https://github.com/exemplar-codes/nextjs-first-tutorial/commit/9568530962a034d500a82e753fb9c82b36d8a631)