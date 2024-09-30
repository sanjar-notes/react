# 18. getByRole
Created Sun Sep 29, 2024 at 10:58 PM

https://testing-library.com/docs/queries/byrole/
## `getByRole`
Role is calculated using the ARIA. [List](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles#:~:text=ARIA%20roles-,Overview,ARIA%3A%20alert%20role,-ARIA%3A%20alertdialog%20role). By default, many tags have semantic elements.

- HTML element - (role)
- `<button>` - `button`
- `<a>` - `link`
- `h1` to `h6` - `heading`
- `<input type="checkbox">` - `checkbox`
- `<input type="radio">` - `radio`
- `<select>` - `combobox`

For elements without a role, the "role" attribute can be add a role.


## `getByRole` options
[Link](https://testing-library.com/docs/queries/byrole/#options)
```jsx
screen.getByRole("role", options={});

// we are talking about option entries
```
The options can help narrow search, and pick unique elements.
- `name` - matches `form.label` or `tag.ariaLabel` or `button.textContent` or `heading.textContent`
- `level` - deals with headings. Values are numbers.
- `hidden`, `checked`, `selected`

## Conclusion
getByRole should be the preferred way to query elements.