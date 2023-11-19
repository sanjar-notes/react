# 8. Platform specific Code
Created Sun Nov 19, 2023 at 5:03 PM

`Platform.OS === 'android'`, i.e conditionals are helpful. But the code is difficult to scale.
RN provides a solution for this.

## `Platform.select()`
Declarative selection of platform stuff.
Generally used for styles, but can be used for any static stuff.

This takes an object as argument.
Each top level key is a platform value - `'ios'`, `'android'`
Returns one of the platform objects.

Used with spreading.
```jsx
const fontStyles = Platform.select({
  ios: {
    fontFamily: 'Avenir',
    fontSize: 20,
  },
  android: {
    fontFamily: 'Roboto',
    fontSize: 18,
  }
});


<View styles={[{ fontWeight: '600' }, fontStyles]}></View>;
```

[Code example](https://github.com/exemplar-codes/DoneWithIt/commit/f3a370b513d6cf04e710b5c982794be25d5da964)
## Cross-platform custom components
Suppose a reusable custom component needs to be made for an app, and it's implementation
would be too convoluted if done via `Platform` API, i.e. there would be too many conditionals.

In such a case, a common structure is to implement the component in a dedicated file per platform.
This avoids `Platform` conditional logic in each file.
Of course, make a `index.js` file that calls these files and has a simple `Platform` logic.

Example: Suppose `<AppButton />` needs to be made this way, then files would be:
- `AppButton/index.js`
- `AppButton.android.js`
- `AppButton.ios.js`
