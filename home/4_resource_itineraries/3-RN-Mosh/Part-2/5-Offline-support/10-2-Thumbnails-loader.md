# 10. 2 Thumbnails loader
Created Sat Dec 30, 2023 at 1:55 PM

If your app is image centric, then showing a normal loading state for images is not a very good UI. Example: if YouTube home list showed loading state for each video, it would look bland.

A simple fix for this is to have an extra image (aka "thumbnail") associated with each actual image on the server. This thumbnail is usually 100x100 pixels.

On the client (our app), when an image component is used, it should fetch both the thumbnail as well as the original image. The thumbnail is quite small and will usually arrive very quickly. We show the thumbnail instead of a loader while the actual image is arriving. This way we show atleast some hint instead of a plain loading state.

## Code
There's no library needed for this. Expo has it already. Use the `placeholder` prop.
```jsx
import { Image } from 'expo-image';

<Image source={url} placeholder={thumnailUrl} />
```

Unfortunately, React Native `loadingIndicatorSource` doesn't work.