# 6. Environment management
Created Sat Dec 30, 2023 at 1:57 PM

Its common to have dev, staging and prod apps.

## How to detect env
```js
import { Constants } from 'expo-constants';

const getCurrentSettings = () => {
  if (__DEV__) return settings.dev; // __DEV__ is from RN core. no import needed.
  if (Constants.manifest.releaseChannel === 'staging') return settings.staging;

  return settings.prod;
}
```

`releaseChannel` is something that is set during app build (or expo publish). where we usually need to specify if staging or prod. See next page for info.

That's it, use a JSON like env library for each config.