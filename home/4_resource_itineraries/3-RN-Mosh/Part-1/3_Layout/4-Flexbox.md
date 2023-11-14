# 4. Flexbox
Created Wed Nov 15, 2023 at 3:49 AM

- Layout via Flexbox is available in RN
- Flexbox styling is exactly like web (browser), except that the default `flexDirection` is "column"
- All components have `display: 'flex'` already applied by default.
- Flex style props
	- `flex`
	- `gap`
	- `flexDirection`
	- `flexBasic`
	- `flexGrow`
	- `flexShrink`
- Since default `flexDirection` is column, a component's height by default is small (same as context). But app screens usually have to atleast be equal to device screen size - the fix is to use `flex: 1` (take all space).