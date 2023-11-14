# 7. Alert
Created Wed Nov 15, 2023 at 12:37 AM

- Used to display an alert popup (modal).
- Cross platform component that renders platform's the native equivalent.

There are 3 variations.
- Direct usage (just like web). No import needed. Shows text in a modal.
	```jsx
	<Button title="Delete" onPress={() => alert("Deleting...")} />
	```
- API usage - buttons. Need to import `Alert`. Shows ctas with title and description.
	```jsx
	import { Alert } from 'react-native';
	
	const onPressHandler = () => 
		Alert.alert("my title", "description", [
			{ text: "Yes", onPress: () => console.log('Yes tapped') }, // primary
			{ text: "No" , onPress: () => console.log('No  tapped') }]); // negative
			// more may be added, primary will render on the left, all else right.
			
	
	<Button title="Delete" onPress={onPressHandler} />
	```
- API usage - text input. Need to import `Alert`. Run callback if 'Ok' is pressed.
	```jsx
	import { Alert } from 'react-native';
	
	const onPressHandler = () => 
		Alert.prompt("my title", "description",
			(enteredText) => console.log('Ok clicked', enteredText)
		);

	<Button title="Delete" onPress={onPressHandler} />
	```
	```jsx
	// text with multiple CTAs.
	import { Alert } from 'react-native';
	
	const onTextMultiCTA = () => 
		Alert.prompt("my title", "description",
			[
			 { text: "Do X", onPress: (text) => console.log('X tapped', { text }) },
			 { text: "Do Y", onPress: (text) => console.log('Y tapped', { text }) },
			 { text: "Do Z", onPress: (text) => console.log('Z tapped', { text }) },
			]
		);
	```

- `Alert.prompt` (text input) works only for iOS
- All of these are APIs, so they can be called even without a UI, like in a `useEffect`.