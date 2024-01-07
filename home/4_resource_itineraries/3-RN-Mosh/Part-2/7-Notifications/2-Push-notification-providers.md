# 2. Push notification providers
Created Sat Dec 30, 2023 at 1:56 PM

## Idea - offload
The idea is simple, our backend app (running the database) does not send notifications directly to the app. Instead there's a middle party - called a push notification service, that gets pinged by our backend app, and then the service sends a notification to the device.

This needs to be done because? Because:
1. **Complexity** - We don't need to care about device info, platform etc. We just store a token from the service.
2. **Cost + efficiency** - Since number of users can be very high, having the database app and the notification code on the same machine doesn't make sense. Push notification services are dedicated for sending notifications, and do so efficiently.

## Providers
aka 'Push notification services'
![](/assets/2-Push-notification-providers-image-1-41c46f41.png)

Expo's push notification service is free. 
And works on both Expo and RNCLI, without any special setup.

Other services are:
- Hard to setup
- Require significant effort to get working
- Plus: Offer more control

That said, Expo does not lock us into using it. FCM and APNs servers can still be [added](https://docs.expo.dev/push-notifications/sending-notifications-custom/#how-to-write-fcm-and-apns-servers).

We'll use expo Push Notification Service for this course.