# 36. Pointer Interactions
Created Mon Sep 30, 2024 at 3:59 PM

## Example
```jsx
import user from "@testing-library/user-event";

render(<Counter />);
const incrementButton = screen.getByRole("button", { name: "Increment" });
await user.click(incrementButton);

const countElement = screen.getByRole("heading");
expect(countElement).toHaveTextContent("1");
```

## Convenience APIs (high level)
`click` isn't the pointer API, its just a convenience API (internally it calls original `click`). There are more:
- `click`
- `dblClick`
- `tripleClick`
- `hover` - for checking hover styles.
- `unhover`
- `tab`

Usage:
```jsx
import user from "@testing-library/user-event";

render(<App />);
user.setup();
await user.dblClick(myButton);
```

## Pointer APIs (low level)
In general, prefer convenience APIs over these lower level Pointer API.
```jsx
user.pointer({ keys: '[MouseLeft]' });
user.pointer('[MouseLeft]'); // if keys is the only arg, pass directy
user.pointer('[MouseLeft][MouseRight]') // press both at the same time
user.pointer('[MouseLeft>]') // click and keep pressed
user.pointer('[/MouseLeft]') // release already pressed mouse button
```

- [Moving a pointer](https://testing-library.com/docs/user-event/pointer#moving-a-pointer)
- [SelectionTarget](https://testing-library.com/docs/user-event/pointer#selectiontarget)

