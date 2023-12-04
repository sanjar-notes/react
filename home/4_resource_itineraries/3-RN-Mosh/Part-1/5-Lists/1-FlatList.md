# 1. FlatList
Created Tue Dec 5, 2023 at 1:40 AM

## Basic
- A performant (virtualized) listing component
- Intended for linear lists
- Cross platform and looks exactly the same.
- Horizontal layout possible.

https://reactnative.dev/docs/flatlist
### Usage and props
```jsx
import { FlatList } from 'react-native';

<FlatList
  data={[{ id: '', name: '', label: ''}]}
  renderItem={(item, index) => <View></View>)}
  keyExtractor={item => item.someIdKey.toString()} // defaults to `id`, then index. toString is important
/>
```

```jsx
// more (optional) props
<FlatList
  // empty, loading state, load more
  refreshing={false}
  ListEmptyComponent ={<SomeComponent />}
  onRefresh={() => {}}


  extraData={} // optional but important, 
  // causes list to re-render if this changes.
  // shallow equals not accepted, just like useEffect
  
  ListHeaderComponent={<SomeComponent />}
  ListFooterComponent={<SomeComponent />}
  ItemSeparatorComponent={<SomeComponent highlighted leadingItem />}
  horizontal={false}
  inverted={false}
/>
```

### Events
 - `onRefresh`

### Methods
- `scrollToEnd({ animated?: true })`
- `scrollToIndex({ index: number, animated?: true, viewPosition: 0_to_1 })`
	- `scrollToItem`
	- `scrollToOffset`

## Pattern
Row click via `onPress` on `renderItem`