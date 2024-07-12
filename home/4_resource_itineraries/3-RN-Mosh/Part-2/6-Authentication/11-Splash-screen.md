# 11. Splash screen
Created Sun Aug 11, 2024 at 8:04 PM

## Problem
Most apps, when they start, make an API call to get the latest user (profile) data. This API call can take a long time, relatively (i.e. may be perceived as sluggish app opening time).

The usual hack is to add a splash screen. A splash screen is a simple screen that doesn't have any input or button. It has the app logo, or some animation. Showing this instead of a blank screen, has been found to be tolerable.

## Code
```jsx
// root screen
import * as SplashScreen from "expo-splash-screen";

const [isReady, setIsReady] = useState(false);

if (!isReady)
  return <SplashScreen 
			startAsync={restoreToken}
			onFinish={() => setIsReady(true)}

return <AppRoutes />;
```

This displays the default splash screen. It can be configured though.

## Configuring expo SplashScreen
1. Add an image in `/assets` folder
2. Edit the `/app.json`, change the `"splash"` property:
	1. `"image": "./app/assets/myImage.png"`
	2. `"resizeMode": "cover"`
	3. `"backgroundColor": "#ffffff"`

Done!