## Navigation in React
It's done using - React Navigation (lib), a very popular lib (has become like de-facto).

An abstraction for 'simple' navigation. Since mobile apps doesn't have a construct of URLs.

The library introduces concepts like
1. "Screens"
2. "name" (analogue of URL/route used in ReactRouter). "/" is not something.
3. "Stack" - it maintains a stack. analogue of History API (of web)
4. Navigator (routes markup). Each element points to a screen component.
	- Supports individual (of course)
	- Supports groups too
5. Programmatic navigation - hooks for it.

Setup
- Provider/wrapper - `Stack.Navigator`

More stuff
1. Navigator can pass `initialParams` to the screen being rendered.
2. Provides some default style for any screen.
3. Screen can be provided with styles `screenOptions`
4. Navigator markup supports two kind of children:
    - Supports individual (of course)
    - Supports groups too. Can be nested.
5. Tab navigation - bottom tabs (e.g. Zomato bottom). `NavigationContainer`, `Tab.Navigator`, `Tab.Screen`
	- how to set up - directly use inside the Navigator (route markup), of course using a component prop.
6. Drawer navigation - side bar (collapsible)
	- how to set up - directly use inside the Navigator (route markup), of course using a component prop.
7. Other navs - there are other things.
8. Combination of stuff - of course, can be done.