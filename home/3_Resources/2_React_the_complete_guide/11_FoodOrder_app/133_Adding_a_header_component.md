# 133. Adding a header component
Created Saturday 25 June 2022

- React, or more correctly, Webpack, requires assets to be imported (via `import` or `require`), and assets don't work normally, like in case of `img src` or `link href`.
```jsx
import imageFile from './image.jpg';
import styles from './stylesheet.css';

function App {
	return 
	(<>
		<link rel="stylesheet" href="../style.css" /> <!-- Won't work -->
		<link rel="stylesheet" href={styles} /> <!-- Works -->
		
		...
		<img src="./image.jpg" /> <!-- Won't work -->
		<img src={imageFile} /> <!-- Works -->
		...
	<>);
}
```