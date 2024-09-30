# 32. Manual Queries
Created Mon Sep 30, 2024 at 1:25 PM

## Why
There are 3 kinds of queries in RTL
- `getBy` and `getByAll`  - throws error
- `queryBy` and `queryByAll` - returns null
- `findBy` and `findByAll` - throws error and is async.

But sometimes, we need more expressive queries (maybe we need to break RTL implementation principle). For these situations, we need something like the DOM API querySelector.

```jsx
screen.querySelector(".hello-class");

// or
const { container } = render(<MyComponent />);
const foo = container.querySelector("[data-foo='bar']");
```

## Discouraged
Using manual queries breaks the RTL philosophy of testing implementation details, so it should be avoided except as a last resort.

## Useful for debugging
Manual queries are quite helpful in debugging/checking RTL code. i.e. when your RTL code does not run, or you are deciding what RTL query to use. Here having a plain `querySelector` is quite helpful since it prevents having to read the generated HTML code.

Examples
- To check if translation library is working or not


## Minor - scoped RTL queries need `within`
- RTL scoped methods require `within`, except for `screen`
- Manual scoped methods do not require `within`. Just like usual DOM
```jsx
import { screen, getByRole } from "@testing-library/react";

// simplest - on document
screen.getByRole(""); // Popular
getByRole(screen, ""); // not idiomatic

// scoped RTL
const { container } = render(<MyComponent />); // or some query
within(container).getByRole(""); // idiomatic
getByRole(container, ""); // not idiomatic

// scoped manual - `within` not needed
const specificElement = container.querySelector(".specific-class");
specificElement.querySelector(); // directly usable

// manual + RTL scoped queries - `within` needed for RTL parts
const specificElement = container.querySelector(".specific-class");
within(specificElement).getByRole("button");
```

Note: 
- for manual queries, you need `render().container`, using `screen` wont do.
- `document` and `render().container` are the same types of things.