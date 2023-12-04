# 7. Icons
Created Sun Nov 19, 2023 at 4:16 PM

## Expo
Expo has the `@expo/vector-icons` [package](https://docs.expo.dev/guides/icons/#expovector-icons) installed by default.
If offers many font sets - Ant Design , Ionicons, MaterialIcons etc.

Steps:
1. Find the icon you want, by name like 'email', 'video', 'person' from the  [sets directory](https://icons.expo.fyi/Index)
2. Choose a set.
3. Import the set component (same name as set name) from `@expo/vector-icons`
4. Use the imported component, with `name` (= email), `size` and `color` props

You're done

Code example:
```jsx
import { MaterialCommunityIcons } from '@expo/vector-icons';

export default MyFeature() {
  return <MaterialCommunityIcons name="email" size={50} color="royalblue" />;
}
```

[Saved in repo](https://github.com/exemplar-codes/DoneWithIt/commit/6b8b357193a5d383124386f4c185542d0443f906)

## RN CLI
One needs to create a wrapper that uses `<Image />`. 
- Exposed props would be `name`, `size` and `color`.
- SVG files would be saved to `/app/assets` and a exporter file can be created `/app/assets/index.js` with entries for each SVG.
- Make sure `fill="currentColor"` in SVGs, so color gets applied to SVG strokes.

Trick for NativeWind controlling size - wrap `Image` by `View` and set Image height and width to 100%.
```jsx
({ src, classes = "w-12 h-12" }) => 
  <View className={classes}>
    <Image width="100%" height="100%" resizeMode="cover"/>
  <View>
```
