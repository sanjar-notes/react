# 17. Progress bar UI
Created Sat Dec 30, 2023 at 1:55 PM

react-native-progress is a general library for progress UI components
Link: https://www.npmjs.com/package/react-native-progress

It works on Expo and RNCLI (no extra steps needed)!

## Code
```jsx
import * as Progress from 'react-native-progress';

{progress < 1 ? 
	<Progress.Bar
	  color='#FF0000'
	  progress={progress} // between 0 and 1
	  width={200} 
	/> 
: null}
```

## Back-sping UI bug
A common bug that's easy to miss in progress components

Make sure to set progress to 0 after it has finished (reached 1). So that when the progress bar renders again, it starts out empty. Do so in the false case of `progress < 1` or in a useEffect if progress has reached 1.

Fortunately, we don't need useEffect since <LottieView /> (the false case of ternary) already has an `onAnimationFinish` that runs when the animation finishes. This is also helpful since once progress reaches 1, the <LottieView /> takes over, and runs the small animation, and we can set progress to 0. Everything is smooth and correct. No useEffect!