# 39. Custom Render Functions
Created Mon Sep 30, 2024 at 5:36 PM

## Situation
It is practically necessary to be able to specify Providers globally instead of at each test case.

[Link](https://testing-library.com/docs/react-testing-library/setup#custom-render)

## How
Simple, override the `render` function itself, and re-export.
```jsx
// setup.jsx
import { render } from "@testing-library/react";
import AllProviders from "./all-providers";

const customRender = (ui, options) => render(ui, { wrapper: AllProviders, ...options});

export { customRender as render };
```