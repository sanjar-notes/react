# 3. Text
Created Tue Nov 14, 2023 at 11:25 PM

- Used for rendering text
- It's the second most important component of RN
- Text is passed as content (child) freely.
- Can have children nodes - Text or otherwise.
- `onPress` event is available.

&nbsp;

- Accepts style props like `color`, `fontSize` etc.
- `numberOfLines={1}` prop can be used for ellipsis. 
	- Default value is 0 (no ellipsis)
	- Pass a width if ellipsis container is smaller than screen
	- [`ellipsizeMode`](https://reactnative.dev/docs/text#ellipsizemode) is a helper prop for dot direction.

```jsx
import { Text } from 'react-native';

function MyComponent() {
  return <Text>Hello, world</Text>;
}
```