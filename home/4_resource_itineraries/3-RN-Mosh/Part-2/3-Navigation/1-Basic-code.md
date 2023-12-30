# 1. Basic code
Created Sat Dec 30, 2023 at 1:54 PM

Code repo: https://github.com/exemplar-codes/DoneWithIt/tree/11-navigation 
## Stack Navigator + general structure
```jsx
const { createStackNavigator } = require("@react-navigation/stack");

const Stack = createStackNavigator();

function MyRootNavigator() {
  return (
    <Stack.Navigator
      initialRouteName=""
      screenOptions={{}} /* lowest priority */
    >
      <Stack.Screen
        name=""
        component={<SimpleReactComponent /> | <SomeNavigatorComponent />}
        options={{}} // highest priority, esp than Navigator.screenOptions
      />
      {/* ... */}
      <Stack.Group screenOptions={{}} /* medium priority */>
        <Stack.Screen />
        <Stack.Screen />
        <Stack.Screen />
      </Stack.Group>
    </Stack.Navigator>
  );
}
```


## Stack ops
1. .navigate (aka replace)
	1. Same - nothing happens
	2. Different (not in stack) - push
	3. Different (in stack) - goes to first occurence and trashes ones at the end.
2. Push
	1. Same - push
	2. Different (not in stack) - push
	3. Different (in stack) - push.
	Comment - simplest

## Programmatic navigation
i.e. by calling function

### For a screen component
By "screen component", I mean one that's passed as a <Screen /> directly to a navigator.
```jsx
// screen component inside a navigator
function MyScreen(props) {
  const { navigation, route } = props; // provided by the library

  // navigate action types
  navigation.navigate;
  navigation.push;
  navigation.pop;

  // navigation action variations
  navigation.navigate("ScreenName");
  navigation.navigate("ScreenName", { anyId: 2 }); // navigate and pass data forward
  navigation.navigate("NavigatorName"); // first screen of some/self navigator
  navigation.navigate("NavigatorName", { screen: "ScreenName" }); // nested navigation
  //some screen in some navigator

  // get data passed during navigation (at destination code)
  route.params.anyId;
}
```

### For a non-screen component
non-screen meaning it's far below the navigator or screen.
Now, RNav does not pass `navigation` and `route` props only till the 1st level.

So, for such non-screen components, use the hooks

```jsx
const navigation = useNavigation(); // get navigation object
const route = useRoute(); // get passed route (at destination)
```
