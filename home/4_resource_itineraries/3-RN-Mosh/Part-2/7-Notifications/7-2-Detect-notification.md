# 7. Detect notification
Created Sat Dec 30, 2023 at 1:56 PM

## Setup
The setup to detect is simple:
1. There's some UI config
2. Hook into the Notification subsystem via Expo's [Notifications](https://docs.expo.dev/versions/latest/sdk/notifications/)package.
3. We store new notification objects from this listening to the store/state.
4. Upon app close (i.e. root level component cleanup), un-hook the listener.
   
Already [seen](https://github.com/exemplar-codes/DoneWithIt/commit/c450f48ff09288f11f6e192b3f75eddb4838ee86#r136427655) in a previous page - we listen for notifications via an event listener and [Notifications](https://docs.expo.dev/versions/latest/sdk/notifications/) expo API. This listener is usually added at the root level component.


## Service response
Received Notification objects has many keys
So, it's a small object - we get response body in .data. 
- `.origin` key has two values - "received" (notification was received when app was in foreground), or "selected" (when app was off or in background, and we tapped the notification). 
 - `.remote` is true for PNS notifications. But it's false for local notifications. 

We'll see how local notifications work soon.