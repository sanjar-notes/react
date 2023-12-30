# 3. Detecting network status
Created Sat Dec 30, 2023 at 1:55 PM

The [react-native-community/netinfo](https://www.npmjs.com/package/@react-native-community/netinfo) library works on Expo. Works on RNCLI too, but minor steps needed for platforms.

It helps get network info like type of network, if internet is reachable and other parameters.

Internally, it pings a 3rd party server (by default Google), but this can be configured.

It's a nice library, exposes main functionality in 3 ways - static method, a hook and an event-listener. Choose whatever you like. Be a little cautious when using event listener though, since forgetting to unsubscribe the event will result in memory leaks.
## Code
```jsx
import NetInfo from "@react-native-community/netinfo";

NetInfo.fetch().then((state) => {
  console.log("Connection type", state.type, state);
  console.log("Is connected?", state.isConnected);
  console.log('as is', state);
});
```

```json
// output
{
  "isConnected": true,
  "isInternetReachable": true,
  "isWifiEnabled": true,
  "type": "wifi",
  "details": {
    "bssid": "02:00:00:00:00:00",
    "frequency": 2447,
    "ipAddress": "10.0.2.16",
    "isConnectionExpensive": false,
    "linkSpeed": 2,
    "rxLinkSpeed": 2,
    "strength": 99,
    "subnet": "255.255.255.0",
    "txLinkSpeed": 2
  }
}
```

Since we're building the react app, the hook is the simplest for us - realtime, and cleans itself up.
```jsx
import { useNetInfo } from "@react-native-community/netinfo";

function MyComponent() {
  const netInfo = useNetInfo(); // same object as above
  const isOffline = !netInfo.isInternetReachable;
  
  // optionally hook accepts a config object as argument
  // see https://www.npmjs.com/package/@react-native-community/netinfo#usenetinfo
  
  return null;
}
```