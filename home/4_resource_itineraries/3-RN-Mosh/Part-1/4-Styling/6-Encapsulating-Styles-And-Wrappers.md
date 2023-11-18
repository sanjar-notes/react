# 6. Encapsulating Styles And Wrappers
Created Sun Nov 19, 2023 at 4:24 AM

## External styles
Since styles are objects (including `StyleSheet.create()`), we can store import/export them like usual JS modules.

Most apps usually have global style file. Feature level style files are also possible, of course.

Sample code:
```js
// app/styles/global.js

// figure out reusable styles, and add here
// Works in an incremental way too - when you discover new common styles during feature, add here
export const layout = {
  screen: { padding: 16, flex: 1 },
  rowItem: { padding: 12, flexDirection: 'column', flex: 1 },
}

export const rounded = {
  md: { borderWidth: 2, borderColor: 'grey', borderRadius: '8' },
  lg: { borderWidth: 2, borderColor: 'grey', borderRadius: '16' }
}

// more
```

```jsx
// app/screens/MyFeature.js

// Makes feature development easy and fast
import styles from '../../styles/global';

function MyFeature() {
  return <View style={styles.rounded.lg}></View>
}
```

## inline vs file vs external styles
- Inline - if style used once on element
- File (Stylesheet) - if style is used by multiple elements of the component (file)
- External - if style is used in multiple files. By external I mean:


there's another variation, see wrapper.

## Wrapper components
If style is used across the codebase, and remains the same for all instances of the component.

The naming convention is to add a small prefix for all wrappers.
Example - `Text` --> `AppText`, or the org name `Text` -> `VPText` (Volopay)

Wrappers are usually stored in `/app/components/core` alongside other custom core components.

## Don't overdo wrappers
The wrappers way is almost non-optional in RN, but don't over do it.

Example: creating a wrapper for `View` doesn't make sense. Same goes with `TouchableOpacity`.

- Doing too much wrappers makes the primitives "look" too abstract, which can be intimidating.
- This affects onboarding time for a new, makes it longer.
- Bugs in wrappers can cause issues at multiple places - an out of control situation.
