# 7. Deleting item aka inner click
Created Tue Dec 5, 2023 at 2:01 AM

![](../../../../../assets/7-Deleting-item-aka-inner-click-image-1-7fd9d830.png)

The inner box needs to prevent bubbling.
```jsx
<Outer onPress={() => "not called"}>
  ...
  <InnerBox
    onStartShouldSetResponder={() => true}
    onTouchEnd={(e) => {
      e.stopPropagation();
      // code
    }}
  />
  ...
</Outer>
```