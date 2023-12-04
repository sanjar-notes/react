# 1. Native feature intro
Created Mon Dec 4, 2023 at 11:53 PM

## Section info
- Going to learn about native device features. Mostly how to access images
- There are very few RN "native features" - `Alert`, `SoftKeyboard` etc. That's it.
- Camera, Contacts, ImagePicker are not available in RN core. But libraries are available for them.
- These libraries have native code and therefore require some platform wise setup (i.e. outside of npm). BTW, this setup is less compared to the past, due to the ['Autolinking'](https://github.com/react-native-community/cli/blob/main/docs/autolinking.md) feature of RNCLI.

## What about Expo projects?
Expo projects are supposed to be JS only projects - they have almost no native code in them, at-least accessible to the developer.

If you want to use a native feature in an expo, there are two possibilities:
1. Expo has a library in its [SDK](https://docs.expo.dev/versions/latest/) that's enough for you. Nice, no extra work needed. Example - [ImagePicker](https://docs.expo.dev/versions/latest/sdk/imagepicker/)
2. Expo doesn't have a library with a feature you want, but an external library is available. Since we're talking about native feature library here, there will be native code in it. There's choice but to eject from Expo. Hard to do, but important if your app uses native features heavily, or you want to ensure high scope of customization of native features. Example - ImagePicker, Contact, FileSystem, DocumentPicker etc.

## Note about Expo native components
- Every 'native' expo component has a compatibility table in docs, as well as extra steps that would be required when you eject from Expo.
- Expo provides very good docs for native libs. And the library list keeps growing