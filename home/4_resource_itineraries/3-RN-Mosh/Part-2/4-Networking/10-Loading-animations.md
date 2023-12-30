# 10. Loading animations
Created Sat Dec 30, 2023 at 1:55 PM

- [Lottie](https://airbnb.design/lottie/) is an animation library from AirBnB
- It can be used in React Native, and works on all platforms.
- The source files are Adobe After Effects file.
	- Many devs don't know After Effects, no issues, head over to https://lottiefiles.com/ and get directly usable files.
	- LottieFiles.com allows editing right inside the website, before download
	- File downloaded is JSON

- Expo provides a [component](https://docs.expo.dev/versions/latest/sdk/lottie/) to render Lottie JSON files
	```jsx
	import LottieView from 'lottie-react-native';
	
	<LottieView source={require('./my-file.json')} />
	```
- LottieView component takes the whole screen space by default. Workaround is simple, just wrap a View around LottieView. Set the height and width on the View.