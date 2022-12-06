# 326. Links
Created Wednesday 7 December 2022

## Why
An SSR app behaves exactly like an SPA after the first load, so we do need client side routing (CSR).


## How
Next.js provides CSR constructs.


## What
Next.js's provides a `Link` component that behaves exactly like React Router's `Link` component, i.e. a CSR link.

- The `Link` uses `href` as the prop for link path .
- `Link.href` should be an absolute path.

Code example:
```jsx
import Link from 'next/link';

function MyArticles() 
{
  /* some code here, if needed */  

  return (
    <div>
	  <ul>
	    <Link href="/next-js-is-good">Next.js is good</Link>
	    <Link href="/next-js-fe-heavy">Next.js is front end heavy</Link>
      </ul>
    </div>
  );
}

export default MyArticles;
```

- For external links or for a code-splitted SSR part of the app, simply use an HTML `a` tag.
- It's not styled as a link, perhaps to avoid confusion with HTML `a` tag.