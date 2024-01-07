# 7. Notifications from the server
Created Sat Dec 30, 2023 at 1:56 PM

1. Install the required SDK for your language from the expo site - Node, Ruby, Python many more are available. 
2. Then make a API request to Expo via the SDK, passing the device's Expo push token (that you typically store during first install of the app) and payload as argument. 
3. Expo service forwards this request to Firebase Messaging or APNS (Apple Push Notification Service), depending on the the device. Finally the device receives the notification. 

Batching of notifications is also possible to avoid own server load.

Example code:
```js
const { Expo } = require("expo-server-sdk");

// example token 'ExponentPushToken[US2xmhFoeM_r-ZzTwWjk8p]', sent as is
const sendPushNotification = async (targetExpoPushToken, message) => {
  const expo = new Expo();
  const chunks = expo.chunkPushNotifications([
    { to: targetExpoPushToken, sound: "default", body: message }
  ]);

  const sendChunks = async () => {
    // This code runs synchronously. We're waiting for each chunk to be send.
    // A better approach is to use Promise.all() and send multiple chunks in parallel.
    chunks.forEach(async chunk => {
      console.log("Sending Chunk", chunk);
      try {
        const tickets = await expo.sendPushNotificationsAsync(chunk);
        console.log("Tickets", tickets);
      } catch (error) {
        console.log("Error sending chunk", error);
      }
    });
  };

  await sendChunks();
};

module.exports = sendPushNotification;

```