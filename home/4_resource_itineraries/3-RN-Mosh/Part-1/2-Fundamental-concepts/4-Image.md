# 4. Image
Created Tue Nov 14, 2023 at 11:44 PM

## `<Image />`
- Core component for rendering images
- Can render both local and network images
- `require()` is needed for network images

```jsx
import { Image } from 'react-native';

function MyComponent() {

  // local image
  <Image source={require("../flag.png")} />;

  // remote image - need to specify dimensions
  <Image source={{ uri: 'https//site.com/flag', width: 200, height: 100 }} />
}
```

- `alt` - description of image used for fallback
- `source`
- `source.uri` - URI of image. Or base64 encoded string equivalent.
- `style` - used for specifying height, width of local images.
- `blurRadius={2}` for blur effect
- Does not have `onPress` event

&nbsp;
- [`resizeMode`](https://reactnative.dev/docs/image#resizemode) - used if fetched image is different from screen size.
- `loadingIndicatorSource`, similar to `source`. Is used to show a image until the image loads
- `onError = (event) => {event.error}` is available.

## `ImageBackground`
A core component for rendering an image in the background with `children` rendering in the foreground.

Usage
```jsx
import { ImageBackground } from "react-native";

<ImageBackground 
  styles={{ flex: 1}}
  source={require("../assets/Welcome.jpg")}
>

  <View>Sign in</View>
  <View>Sign up</View>
  <View>Privacy policy</View>
</ImageBackground>
```