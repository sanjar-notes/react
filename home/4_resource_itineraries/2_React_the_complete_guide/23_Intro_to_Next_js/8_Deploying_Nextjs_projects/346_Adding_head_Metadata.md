# 346. Adding "head" Metadata
Created Sunday 25 December 2022


## Why
Add dynamic page title and metadata inside HTML `head` tag.

It is important:
1. Generally - tab name, accessibility, semantic web.
2. SEO - one of the most important reason Next.js is used. The `head` tag is responsible for:
	1. Search result title - `title` tag. Also add a `<meta name="title" />` with the value same as `title`.
	2. Search result description - `<meta name="description" />` tag.
	3. Other meta tags, used for SEO, promotion, counting CTR (click-through-rate).

Example - code:
```HTML
<head>
  <title>Academind</title>
  <meta name="title" content="Academind" />
  <meta
    name="description"
    content="Academind offers hundreds of coding tutorials ..."
  />
</head>
```

Example - output:
![](../../../../../assets/Pasted%20image%2020221225014714.png)


## How
Use a React portal to add stuff to the `head` tag.


## What
Next.js has a `Head` component that does exactly this. It portals it's children to the HTML `head` tag.

It can be used in any UI component (including non-page components and non-pre rendered UI), just remember to add `title` and/or `meta` tags as children.

```js
import Head from 'next/head';

export default MyPage() {
  return (
    <>
	  <Head> 
		<title>Home page</title>
		<meta name="page destination" content="Home page" />
		<meta name="language" content="en-us" />
	  </Head>
	  <div></div>
	</>
  );
}
```
[Code example](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/e40ee3fcd3bffd6129c75a9484d5fffe4c147aed)

- As said, `Head` can be used in any UI component, including non-page and/or non-pre-rendered ones. [Code example - set tab title dynamically on the client](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/f492bc5b7a208956bdf1509b368aaa81255cfb48).
- If the UI tree has multiple `Head`, the final `head` tag is the result of additively combining all `Head` nodes in pre-order traversal fashion, with newer `Head` instances overriding existing tags. [Code - multiple `Head` components](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/396df5f48d6aa5083e684c68cfe9d86413a5a5b1)
- DRY - we can add `Head` component in `pages/_app.js` and conditionally set the children of `Head` based on the `router` prop that the "root" component has access to. Evaluation order for multiple `Head` still holds, so it would be easy to add a custom `Head` if at all needed. [Code](https://github.com/exemplar-codes/nextjs-first-realistic-tutorial/commit/e5a7d5d90f8b0e03ce1fd14cc8eb63a321558e6c)
