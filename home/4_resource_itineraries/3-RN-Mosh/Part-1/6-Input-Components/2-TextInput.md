# 2. TextInput
Created Tue Dec 5, 2023 at 1:02 AM

https://reactnative.dev/docs/textinput

## Basic
- RN core's input text box
- By default its invisible.
- Cross platform but renders according to the platform

```jsx
import { TextInput } from 'react-native';

<TextInput
  value=""
  onChangeText={(newText) => {}}

  placeholder=""
  keyboardType="numeric" // | 'dialpad' | 'default'
  maxLength={10}

  clearButtonMode="never" // 'while-editing' | 'unless-editing' | 'always'
/>
```
- `clearButtonMode` is iOS only. It renders a right "cross"/"clear" icon.


## Wrapper usually needed
Projects usually have a wrapper they use (instead of directly using `<TextInput />`)

Reason being that `<TextInput />` has no styles (invisible) by default. And also that RN has no style inheritance.