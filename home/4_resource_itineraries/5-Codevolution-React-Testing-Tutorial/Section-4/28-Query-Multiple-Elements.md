# 28. Query Multiple Elements
Created Mon Sep 30, 2024 at 11:56 AM

The `getBy` queries are for matching unique (single) elements only. If there could be multiple matching elements, its better to use `getAllBy` variations. This returns an array or throws an error (if none found).

> Get quickly, Query casually, Find eventually.


## Example
```jsx
const skills = ["HTML", "CSS", "JavaScript"];

test ('renders a list of skills', () => {
	render (<Skills skills={skills) />);
	const listItemElements = screen.getAllByRole("listitem");
	expect(listItemElements).toHaveLength(3); // btw, OK
	
	expect(listItemElements).toHaveLength(skills.length); // btw, better
}
```