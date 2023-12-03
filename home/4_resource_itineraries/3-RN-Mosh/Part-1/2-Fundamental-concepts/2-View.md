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

[Ready to use component](https://github.com/exemplar-codes/DoneWithIt/commit/29779a0cc1fa906b1c7f6eff4f43a6900d296354)

- This is also a core component. Almost exactly like `View`.
- Its used to prevent overflow of app UI into the system UI (top bar, navigation bar).
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

## `ScrollView`
By default `View` takes full width, but just content height. i.e. "align stretch" and "justify start".

Even if content is too large, the `View` does not get a scroll bar, i.e. the extra content is just inaccessible.

`ScrollView` is a core component that solves this problem.

Props:
- `contentContainerStyle` - for style. usual `styles` doesn't work.
- Scroll direction - `horizontal`, `vertical` boolean props. Only one direction at a time. Default `vertical`

Major quirk and workaround:
- By default, it takes the whole height (and whole width, like View). To fix the height issue, especially in horizontal mode, just wrap the `ScrollView` with a `View` and set `ScrollView`'s height to be "100%". Nice hack. [See code](https://github.com/exemplar-codes/DoneWithIt/commit/eedf8ca18bc2e352505c18a9c725284bc8b599da).

Events
- `onScroll`: `e.nativeEvent.contentOffset` is {x, y} = scrolled distance. (initially 0, max=overflow_size). `.contentSize`, `.layoutMeasurement` is also available, which give the large vs fixed size, respectively.
- `onContentSizeChange`: `e` = new size (a number)

Methods (via ref):
1. `ref.current.scrollTo({ x, y, animated: true })`
2. `ref.current.scrollToEnd({animated})` - helpful since don't have to calculate ScrollView size manually. For start `scrollTo({ x: 0 })` would do.

FIXME: for scroll in both directions, a normal (vertical) `ScrollView`  with each child being a `horizontal` a ScrollView works.

ScrollView is quite powerful, and has snapping capabilities too, see [docs](https://reactnative.dev/docs/scrollview#removeclippedsubviews)- the most essential being `snapToOffsets`