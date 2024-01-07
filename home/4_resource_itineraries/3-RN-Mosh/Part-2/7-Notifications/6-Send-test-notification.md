# 6. Send test notification
Created Sun Jan 7, 2024 at 6:24 PM

## From Expo online tool
Use the expo site tool to send notifications. 

There's a gotcha here: `send {"_displayInForeground": true }` atleast, otherwise there won't be a notification. 


## From app (client) itself
It's possible to ping Expo notification service from the app itself, and receive the notification. Here's the code
```js
const sendNotificationHandler = async () => {
  await Notifications.scheduleNotificationAsync({
    content: {
      title: "You've got mail! 📬",
      body: "Here is the notification body",
      data: { data: "goes here" },
    },
    trigger: { seconds: 2 },
  });
  
  console.log("Server pinged fine");
  setIsLoading(true);
  setTimeout(() => {
    console.log("Sould have gotten it by now");
    setIsLoading(false);
  }, 2000);
}; // client pinging self, not common. for demo purposes.
```