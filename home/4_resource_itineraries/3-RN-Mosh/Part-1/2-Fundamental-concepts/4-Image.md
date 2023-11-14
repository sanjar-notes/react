# 4. Image
Created Tue Nov 14, 2023 at 11:44 PM

- Core component for rendering images
- Can render both local and remote images
- Can also render image fro local disk (Camera photos)

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


&nbsp;
- `loadingIndicatorSource`, similar to `source`. Is used to show a image until the image loads
- `onError = (event) => {event.error}` is available.