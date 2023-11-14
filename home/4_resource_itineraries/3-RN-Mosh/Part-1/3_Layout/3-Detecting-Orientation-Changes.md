# 3. Detecting Orientation Changes
Created Wed Nov 15, 2023 at 3:30 AM

To detect realtime orientation of the device, a hook [`useDeviceOrientation`](https://github.com/react-native-community/hooks#usedeviceorientation) is available. 

Steps to use:
1. `npm install @react-native-community/hooks`
2. Code
	```js
	import { useDeviceOrientation } from '@/react-native-community/hooks';

	function MyComponent() {
	  const orientationValue = useDeviceOrientation(); // 'portrait' | 'landscape'

	  return null;
	}
	```