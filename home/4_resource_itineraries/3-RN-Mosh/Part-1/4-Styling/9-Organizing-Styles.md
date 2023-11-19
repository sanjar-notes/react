# 9. Organizing Styles
Created Sun Nov 19, 2023 at 6:29 PM

Mostly the same as [6-Encapsulating-Styles-And-Wrappers](6-Encapsulating-Styles-And-Wrappers.md)

## Where to keep local styles
There are two approaches
- One file - `MyComponent.js`. Has the component, as well a top level `styles` variable (created using `StylesSheet.create`)
- Two files - `MyComponent/index.js` and `MyComponent/styles.js`, the index file imports styles from "styles.js", which has the style object created using `StyleSheet.create`

Many devs prefer the second, because it separates functionality from presentation.
But many devs also prefer the first approach, since it's concise.

Choose whatever you like. The only thing that matters is being consistent - use one way and do so across the codebase.