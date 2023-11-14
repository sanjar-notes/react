- if you're serious (long term) - prefer RNCLI over ExpoGo.
- Pages (web) <--> Screens (android)
- Core component - View (non-scroll div), ScrollView (normal div) Text, Image. Docs are good.
- ScrollView - 


## Styling in RN
- Syntaxes:
    1. inline
    2. `StyleSheet`
- Where to keep styles - there are two philosophies:
    1. Too much use - move to global file. e.g. colors, card-wrapper. ESM import to use.
    2. Local one time use - in same file.
- Flex is there. Behaves a little diff from web, default direction is `column`.
- Grid - there's no official grid.
    - Workaround `FlatList` has a `numsColumns`
    - Use flex with a little more deliberate styling.


## Basic Components
1. `View` props (most used) - `role`, `style`, `onClick` (`onPress`) event
	- do `flex-1` for full space. Otherwise it's invisible. Weird ritual, but fixes it? FIXME.
2. `Text` - `numberOfLine` (auto ellipsize) auto, ellipsizeMode - head, tail, middle, clip. `selectionColor`
3. `Image`
    - accpets `source` as PNG only. If local do `require('../path_to_local')`. pass HTTPS url directly. PNG makes some sense since max size of mobile devices isn't very high.
    - ImageWrapper Ashish made, that does `require` or no change by checking `url` links (`.startsWith()`)
    - onLoad, and other image state handlers are present
    - `srcSet`
    - `blurRadius` prop - will blur the image.
    - For background image - don't do `w-full` and position. But wrap your UI with `ImageBackground` RN component.


## Button
- For building own button, people use `TouchableOpacity` over `Button`
- why? `Button` (like web `<button></button>`) picks platform button vs `TouchableOPacity` (`<div>` with `<button>` props) (custom button).
- There are some components here:
	- `TouchableOpacity` - shows 'click' animation styling on press. Non platform button (but has animation).
	- `TouchableHighlight` - minimum animation (only BG color changes)
	- `TouchableOpacityWithoutFeedback` - doesn't show any animation on user press.

## Switch
- Philosophy - Core `Switch` is good enough.

## Text-Input
- Usual text input box.
- Normal props are there.
- Some props are are platform specific (i.e. will be ignored in other platform).
- `type`, `numeric`, `autoCapitalize`, prop affects the keyboard input. Of course, won't work in Android keypad phone.
- `visible-password` prop for password
- Confirm button icon - don't know. FIXME


## Dropdown
No native stable. Recommendation of packages to use.


## Listings
1. `ScrollView` - ok, but no virtualization. `.map` works. Not a listing component btw, just a scrollable view.
	- Supports both way (hori and verti) scroll ? FIXME
	- UX perspective - try to use your scroll on one axis only (vertical for phones, e.g.)
1. `FlatList` - ScrollView with virtualization. data
   - Meant for lists
   - `map` doesn't work with this. Have to pass control over to it, using `data`, `renderItem`, `keyExtractor` props
   - `extraData` can be used to `re-render` (motivation, how this came to be?)
   - `snapToEnd` (scroll to end if in the middle, till a threshold)
2. `SectionList` (example - contact list with A-Z)
	- data props -` [{sectionTitle, [{title}, {title}]}, {sectionTitle, [{title}, {title}]}]`
	- takes prop to vary header section UI and other things
	- Is virtualized by default. non-virtual variant does not exist.
	- sticky section header (when scrolled past) prop is there. But default value is different based on platform.
3. `VirtualizedList`  - (`FlatList`'s base component). Not used on it's own/

note: prefer ScrollView for screen UI only, not listing.


## Utility components
1. `KeyboardAvoidingView` - when platform keyboard opens, move the view up (can configure). To use, just wrap the UI with this. Use the `behavior` prop (recommended).
2. `SaveAreaView` - prevents overflow to Android system UI.
3. `Alert` (system level Modal) - `text`, `onPress` and `style`
4. `Modal` (custom level modal) - animationType, and other stuff. Provided out of the box. Android isn't that pretty, ios is good.
5. `Pressable` - gesture detection (has more gesture that View.onPress or other usual things), like swap, zoom etc.
	- Is usually a wrapper to your UI
	- But can show `ripple` effect, sound effect etc. Props are there.






# General RN
## Platform specific code (`Platform`)
In some cases - RN recommends platform specific code.
```jsx
import {Platform} from 'react-native';

export default function MyComponent() {
	return 
	<Text>{Platform.os === 'ios' ? 'On Apple' : 'Not on Apple'}</Text>
}
```


## Knowledge of RN
- Almost anything can be created by `View`, `TouchableOpacity`
- Negative margin isn't supported on RN, as of now (Aug 2023).


