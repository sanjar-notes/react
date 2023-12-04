# 15. Getting Location
Created Tue Dec 5, 2023 at 12:38 AM

[`expo-location`](https://docs.expo.dev/versions/latest/sdk/location/) library is available.

Usage flow is the same as ImageLibrary - request, launch

```jsx
import React from "react";
import * as Location from "expo-location";
import { Button, View } from "react-native";

export default function App() {
  const permissionFlow = async () => {
    const { granted } = await Location.requestForegroundPermissionsAsync(); // acceptable
    // .requestBackgroundPermissionsAsync less private
    
    console.log(granted);
  };

  const locationFlow = async () => {
    const result = await Location.getLastKnownPositionAsync(); // almost instant
    // .getCurrentPositionAsync takes some time (~5 seconds)
    
    // coords.latitude, coords.longitude, coords.heading

    console.log(result);
    
    const sample_result = {
      coords: {
        accuracy: 100,
        altitude: 0,
        altitudeAccuracy: 0,
        heading: 0,
        latitude: 37.4226711,
        longitude: -122.0849872,
        speed: 0,
      },
      mocked: false,
      timestamp: 1701717475116,
    };
  };

  return (
    <View style={{ paddingTop: 100 }}>
      <Button title="Permission flow" onPress={permissionFlow} />
      <Button title="Location flow" onPress={locationFlow} />
    </View>
  );
}
```