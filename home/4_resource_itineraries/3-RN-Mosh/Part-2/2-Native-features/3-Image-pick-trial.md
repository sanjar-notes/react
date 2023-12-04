# 1. Image pick trial
Created Wed Nov 29, 2023 at 1:17 AM

- [`expo-image-picker`](https://docs.expo.dev/versions/latest/sdk/imagepicker/#imagepickeroptions) allows image selection from camera and local storage

## Permission via picker library
The ImagePicker library provides a static function that returns status of the permission. It's async and results can vary depending upon what the user selected for permissions.

There are two steps:
1. `request*` - this is done before any native op. The permission status is returned. If permission was never asked, the user gets a user prompt to select permission. If permission was answered, it will be available in the future without a prompt. If permission is false, show an alert. Otherwise continue.
2. `launch*` - assuming permission is given, this function launches the native feature flow. At the end of the flow, one received URI or other data pertaining to the flow.
### Camera
```jsx
import React from "react";
import * as ImagePicker from "expo-image-picker";
import { Button, View } from "react-native";

export default function App() {
  const permissionFlow = async () => {
    const { granted } = await ImagePicker.requestCameraPermissionsAsync();
    console.log(granted);
  };

  const cameraFlow = async () => {
    const { assets, canceled } = await ImagePicker.launchCameraAsync();
    const { uri, height, width } = assets[0];
    console.log(uri, height, width);
  };

  return (
    <View>
      <Button title="Permission flow" onPress={permissionFlow} />
      <Button title="Camera flow" onPress={cameraFlow} />
    </View>
  );
}
```


### Image Library (aka Gallery)
```jsx
import React from "react";
import * as ImagePicker from "expo-image-picker";
import { Button, View } from "react-native";

export default function App() {
  const permissionFlow = async () => {
    const { granted } = await ImagePicker.requestMediaLibraryPermissionsAsync();
    console.log(granted);
  };

  const cameraFlow = async () => {
    const { assets, canceled = false } = await ImagePicker.launchImageLibraryAsync({
      allowsMultipleSelection: true, // default false
    });
    console.log(assets);
    const { uri, height, width } = assets[0];
    console.log(uri, height, width);
  };

  return (
    <View style={{ paddingTop: 100 }}>
      <Button title="Permission flow" onPress={permissionFlow} />
      <Button title="Camera flow" onPress={cameraFlow} />
    </View>
  );
}
```


## A note about Permissions in Expo
Expo used to have a global `expo-permissions` library that could ask for any permission. But this has been deprecated. Permissions are now available in the respective library - ImagePicker, Audio, MediaLibrary.

All these have the same code flow - `.request*` and `.launch*`.

## Exercise - build scrollable image picker
https://github.com/exemplar-codes/DoneWithIt/commit/6efcbdaf20b1a92821b626ae570a1bc493f960c2

Learnt:
1. ImagePicker permission function
2. Structure of added assets and how to display them. The imp thing is `uri`
3. Learnt about `BackHandler` API, applicable for Android only. Has add listener API. Does take into account multiple presses (I didn't consider this though).
4. ScrollView - height gotcha, onScroll, snapToOffset, ref.current.scrollToEnd etc

Branch: https://github.com/exemplar-codes/DoneWithIt/tree/rn2/image-form-exercise