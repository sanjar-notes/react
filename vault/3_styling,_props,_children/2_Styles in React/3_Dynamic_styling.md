# 3. Dynamic styling
Created Sunday 13 February 2022

- For inline styles, we can use a ternary expression, AND/OR operator, format strings to set values/whole `style` object. Example:
```jsx
<div style={isValid ? {color: "red"} : {color: "black"}}>
	...
</div>


// OR equivalent, but shorter
<div style={{color: isValid ? "red" : "black"}}>
	...
</div>


// OR
let style = {{color: "black"}};
if (isValid)
	style.color = "red";

<div style={style}>
	...
</div>
```
- For imported CSS file, we can change `className` attribute dynamically, like we did for inline styles.