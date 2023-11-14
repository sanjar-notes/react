# 5. Touchables
Created Wed Nov 15, 2023 at 12:08 AM

- These are some wrapper components meant to be clicked/tapped by the user
- There are 3:
	1. `TouchableOpacity` - on tap, does whitening (opacity of content is reduced)
	2. `TouchableHighlight` - on tap, does darkening (background is darkened).
	3. `TouchableOpacityWithoutFeedback` -  on tap, no UI change. Try to [avoid](https://reactnative.dev/docs/touchablewithoutfeedback) this unless necessary.
	4. `TouchableNativeFeedback` - on tap, animates acc to stock Android UI. Only available for Android.
- All have these events:
	- `onPress`
	- `onLongPress`
- Btw, `View` has no `onPressEvent`