# 8. StyleSheet
Created Wed Nov 15, 2023 at 1:08 AM

- RN core construct for reusing styles.
- This is an alternative way to style in RN, in addition to the inline `style={{}}` prop.
- The effect is the same as inline styles.
`Stylesheet.create()` takes multiple style 'keys' that may be used.

```jsx
import { StyleSheet } from 'react-native';

const myStyles = StyleSheet.create({ 
	mySection: { marginTop: 24, padding: 16 },
	myHeading: { color: "blue", fontSize: 48 }
});

function MyComponent() {
	return <View>
		<View style={myStyles.mySection}>
		  <Text style={myStyles.myHeading}>Heading 1</Text>
		</View>
		
		<View style={myStyles.mySection}>
		  <Text style={myStyles.myHeading}>Heading 2</Text>
		</View>
	</View>;
}
```

- Can be exported and reused in other files
- Generally used outside the component function, since styles remain static, and conditional ones are created beforehand. Saves some re-render compute.


## Why use StyleSheet
1. Reuse aka DRY
2. For style validation checks: 2nd level keys inside StyleSheet config are checked by RN, for typos.
3. Leaves scope for internal RN optimization, if it's implemented in the library later.