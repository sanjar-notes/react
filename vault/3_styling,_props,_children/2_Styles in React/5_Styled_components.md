# 5. Styled components
Created Sunday 13 February 2022

### Why
- For very large projects, where many people work together, class and CSS code can clash, because it's applicable globally - for CSS files that are imported.
- Basically, we need a way to scope styles to the component only, so that it doesn't affect any other component. This is achieved using styled components.

### How
- Styles for a component are defined inside the component file. We don't import CSS files as we have done previously.
- HTML tags are inherited from [the library](https://styled-components.com/) and styles are provided for them, if needed. These inherited tags are stored in variables, which are then used instead of the primitive tags.
- When the project is built and assets are generated, the classname are hashed, so that they don't class. This makes the final HTML classes cryptic, but it's fine.

### What
**Dependency**: We need the `styled-components` package installed. Install it in the project using `npm install --save styled-components`.

Steps to use `styled-components`:
1. Import `styled` object from the `styled-components` library, like so:
```jsx
import styled from 'styled-components';
```
2. Specify the styles for each tag inside the file. Provide a name for each tag. As the tag is already selected, there's no need for a selector/class. Of course, pseudo-selectors can be specified, using `&`. Directly specify the styles for tags like so:
```jsx
const Div = styled.div`
	color: red;
	background-color: salmon;

	&:hover
	{
		color: black;
	}
`

// now use <Div></Div> instead of <div></div> here.
```

#### About styled components
- Props on styled components are passed down as is to the HTML elements, so `onClick` and other attributes work normally.