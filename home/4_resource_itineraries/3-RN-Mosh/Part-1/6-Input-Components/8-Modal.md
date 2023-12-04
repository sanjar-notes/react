# 8. Modal
Created Tue Dec 5, 2023 at 1:17 AM

RN core has `Modal`
## Basic
It's just a wrapper for content.
Renders on top of existing UI. Covers the entire screen.
```jsx
import { Modal } from "react-native";

<Modal
  visible={false}

  transparent // optional. Default false (background is hidden completely).
  onShow={() => {}}
  animationType="none" // 'slide' | 'fade'
>

</Modal>
```
- `style` prop not available. To add background color, add a `View` inside with `flex=1` and `opacity=0.5` (anything < 1) and move modal content inside it.

## Example
Transparent background example.
```jsx
import React, { useState } from "react";
import { View, Modal, Button, Text } from "react-native";

export default function App() {
  const [showModal, setShowModal] = useState();
  const toggleModal = () => setShowModal((_) => !_);

  return (
    <View
      style={{
        flex: 1,
        alignItems: "center",
        justifyContent: "center",
        gap: 100,
      }}
    >
      <Button title="Open modal" onPress={toggleModal} />

      <Modal visible={showModal} transparent>
        <View
          style={{
            flex: 1,
            backgroundColor: "gold",
            alignItems: "center",
            justifyContent: "center",
            opacity: 0.6,
            gap: 80,
          }}
        >
          <Button title="Close modal" onPress={toggleModal} />
        </View>
      </Modal>

      <Text>
        loremqdblqywdfdqwdloremqdblqywdfdqwdloremqdblqywdfdqwdlo
        remqdblqywdfdqwdloremqdblqywdfdqwdloremqdblqywdfdqwdlo
        remqdblqywdfdqwdloremqdb lqywdfdqwdloremqdblqywdfdqwdlor
      </Text>
    </View>
  );
}

```