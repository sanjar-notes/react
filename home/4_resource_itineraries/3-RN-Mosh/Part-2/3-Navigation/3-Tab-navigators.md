# 3. Tab navigators
Created Sat Dec 30, 2023 at 1:54 PM

These are another type of navigators.
They render at the bottom as a row. With each cell being clickable.

- Tabs have independent state, which persists across "jumps", there's no pop or destroy action since it's not a stack. There's no duplicates (and traverse back via back button) either.
- Navigation props and programmatic navigations happens exactly like in Stack Navigator
- Tabs usually mean addition of a UI feature where the navigator itself is also visible (bottom in this case). This is different from the StackNavigator, which had no navigation UI, and just presented complete screens.
- The style (cell style) config is a single prop on the navigator itself. There's no <Screen /> wise prop styling.
- The specific tab config (like icon) is specified on the TabScreen, and callback type prop ares still available on Screens for dynamic stuff like title, badge count. This callback also contains "recommended" UI values like `size`, `color` that may be used as is.