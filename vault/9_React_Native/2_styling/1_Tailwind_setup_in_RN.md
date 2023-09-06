# Tailwind setup in RN
Created Wednesday 6 September 2023

## Library (s) to use
1. [NativeWind](https://www.nativewind.dev/) - simplest. code stays the same as web. `className` prop with string.
2. [twrnc](https://www.npmjs.com/package/twrnc) - also good, but syntax is a little more involved `<Text style={tw`text-red-600`} />`


## NativeWind features
 App code (looks the same as web):
```jsx
<Text className="text-yoursystem-500">
  Hello bro (native wind) {new Date().toLocaleTimeString()}
</Text>
<Text className="text-danger-500">
  Hello bro (native wind red) {new Date().toLocaleTimeString()}
</Text>
```
Claimed features:
- Works on all RN platforms, uses the best style system for **each platform**.
- Uses the Tailwind CSS compiler
- Styles are computed at build time
- Small runtime keeps your components fast
- Babel plugin for simple setup and improving **intellisense** support. *checked: works!*
- Respects all **tailwind.config.js** settings, including themes, custom values, plugins. *checked: works!*
- dark mode / arbitrary classes / media queries
- **pseudo classes** - hover / focus / active on compatible components (docs). *checked: works!*
- **styling based on parent state** - automatically style children based upon parent pseudo classes (docs)
- children styles - create simple layouts based upon parent class

For arbitrary values - colors like `text-[red]` doesn't work, but sizing like `w-[100px]` does work. This is practically fine, since color system is a much "visible" thing than spacing, and so, is usually enforced more strictly in the design system.

## Setup for NativeWind
- Follow the [quickstart](https://www.nativewind.dev/quick-starts/react-native-cli) steps.
- In `tailwind.config.js`, replace the first (commented import) by this:
  ```js
  /** @type {import('tailwindcss').Config} */ // remove
  const defaultTheme = require("tailwindcss/defaultTheme"); // add
  ```
- Tailwind config properties work like web - colors, fonts etc.


## Common problems and fixes
1. "process(cb)" issue - two steps here:
	1. Lower the version to 3.2.2 [StackOverflow](https://stackoverflow.com/a/76700786/11392807)
	2. If the issue persists, a restart will fix.