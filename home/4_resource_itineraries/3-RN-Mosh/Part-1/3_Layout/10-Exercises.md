# 10. Exercises
Created Thu Nov 16, 2023 at 2:15 AM

## Tip - create a `app`/`src` folder
- After initializing the project code with Expo.
	- Make an `src` or `app` folder and move important code there. This will be helpful if we eject from expo, create a new project with copied code, or move to a different tooling for RN. 
	- Update `app.json` paths for moved files.
	- Move `/assets` into `src`
- General structure of `src`
	- `assets`
	- `screens` (aka 'pages' in web)
	- `components`

## Exercise 1 - WelcomeScreen
![](../../../../../assets/Pasted-image-20231118232608.png)
Lessons
- Work with images, esp in the background
- `width`/`height` for fixing dimensions as opposed to `basis`/`grow`/`shrink`

[Code](https://github.com/exemplar-codes/DoneWithIt/commit/3219f8765c06e53c7a6964487a74b236205373a5)

## Exercise 2 - ViewImageScreen
Lessons:
- Prevent app UI overflow into system
- Fixing image sizes (esp big to small) - `<Image resizeMethod="scale" />`

![](../../../../../assets/Pasted-image-20231118232621.png)

[Code](https://github.com/exemplar-codes/DoneWithIt/commit/c1cba8525377f03ccc8144c694f30199bdfad76f)

## Tip - enums, colors
Colors and enums, especially business logic ones should be stored in `/app/constants/`
```jsx
// product.js
export const ORDER_TYPES = {
  PREPAID: 'prepaid',
  COD: 'cash-on-delivery',
}

export const PRODUCT_MODULES = {
  EXPLORE: 'explore',
  ORDER: 'order',
  PAYMENT: 'payment',
  HELP: 'help',
  TRACK_ORDER: 'track-order'
}
```

```jsx
export const COLORS = {
  DARK: '#000000',
  LIGHT: '#fffff',
  PRIMARY: '#ff0000',
  SECONDARY: '#0000ff',
}
```

This helps us:
1. Avoid typo bugs, and provides auto-completes
2. Some light documentation for variations of product
3. Searching code faster, when a module or variation breaks