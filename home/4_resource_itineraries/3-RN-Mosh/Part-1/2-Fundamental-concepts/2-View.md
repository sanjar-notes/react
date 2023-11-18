# 2. View
Created Tue Nov 14, 2023 at 11:25 PM

## `View`
- Most fundamental core component
- Used for grouping nodes.
- UI styling like padding, flex, border etc are applicable, of course.
- Has `onPress` event handler.
- It cannot render text (directly). Also, font styles on this don't work.

```jsx
import { View } from 'react-native';

function MyComponent() {
  return <View></View>;
}
```

- Optionally, has `nativeId` prop that can be used to [locate](https://stackoverflow.com/questions/52483374/can-i-use-the-prop-nativeid-to-locate-a-view-in-native-code) element in native module code (Kotlin).
- Has many non-manual or special event handlers.

## `SafeAreaView` (ios only)
- This is also a core component. Almost exactly like `View`.
- Used to prevent overflow of app UI into the system UI (top bar, navigation bar).
- It only works for iOS, and is used to avoid the top notch for newer iPhones. For Android a hack needs to be done.

- Use when: if the app UI for a screen is flowing onto system UI. Then wrap the component with `SafeAreaView`. That's it.

- Should be used as a top level wrapper? By default, no.
	- Yes - if the app is intended to never flow into system UI. Wrapper is fine.
	- No - if app asymmetric behavior, i.e. has some screens that are intended to flow into system UI, then per screen wrapping should be done.

- For Android, `SafeAreaView` behaves exactly like `View`. the workaround for overflow protection is `StatusBar.currentHeight`:
	```jsx
	import { StatusBar } from 'react-native';
	
	return <View styles={{ marginTop: StatusBar.currentHeight }}></View>
	```
	 This doesn't affect iOS though. So if the target is both Android and iOS, both `SafeAreaView` and `StatusBar.currentHeight` (conditional based `Platform`) are used.