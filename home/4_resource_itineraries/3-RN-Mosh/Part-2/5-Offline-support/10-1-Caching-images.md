# 10. 1 Caching images
Created Sat Dec 30, 2023 at 1:55 PM

We can save strings in AsyncStorage fine.

But what about images or assets? How do we store them for caching?

---
It's not possible with AsyncStorage, since images and assets are binary data, and are usually large in size.

For image caching, there are libraries. The usual pattern here is that the library provide a near identical replacement for RN core image, This way the library intercepts, caches and presents fetched images.


- react-native-expo-image-cache (expo-blur needs to be installed before for this to work) is a library. *DOEST WORK/NOT-PREFERRED*. The `expo-image`'s [Image](https://docs.expo.dev/versions/latest/sdk/image/#cachepolicy) could help.
- [react-native-fast-image](https://www.npmjs.com/package/react-native-fast-image) is a library for RNCLI, that provides a replacement for RN core Image. This way it's able to cache images. The library also has more useful features