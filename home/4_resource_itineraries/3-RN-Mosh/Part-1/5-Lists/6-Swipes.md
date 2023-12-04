# 6. Swipes
Created Tue Dec 5, 2023 at 1:56 AM

- Install `react-native-gesure-handler`
- Wrap each `renderItem` with `<Swipeable></Swipeable>`

```jsx
<Swipeable 
  renderRightAction={(item) => <SomeComponent onPress={} />}
  renderLeftAction ={(item) => <SomeComponent onPress={} />}
>
</Swipeable>
```
