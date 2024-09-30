# 33. Debugging
Created Mon Sep 30, 2024 at 2:37 PM

## Printing the tree/element
```jsx
import { screen } from "@testing-library/react";
screen.debug(); // prints whole tree

import { prettyDOM } from "@testing-library/react";
const myElement = screen.getByRole();
console.log(prettyDOM(myElement)) // prints selected container
```
- `screen.debug()` prints the whole DOM tree.
- `console.log(prettyDOM(element))` for printing specific element.

## Print roles
```jsx
import { logRoles } from "@testing-library/react";

const view = render(<App />);
logRoles(view.container); // logs all ARIA roles
```

This can be used to find roles without reading the app code.