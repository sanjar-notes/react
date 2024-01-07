# 3. Flow
Created Sat Dec 30, 2023 at 1:56 PM

actually just the flow architecture for our app (client + server if any). We're not concerned with how the provider works.

Expo steps:
1. Register the app (and device) with Expo directly, to get a token. This happens on the device itself and usually happens through a prompt 'Allow'.
2. Send and store token received from Expo (step 1) on 'your server'.
3. Send a notification to the device from your server. This is done by pinging Expo Push Notification service, which then sends a notification to the app. Expo provides server SDK's to do this, good.
4. Handle the notification on the client.

Step 1 needs to be done only once per user+device combo. If the app is uninstalled by the user, push notifications may be pushed by our server, but Expo will let us know that nobody received it (FIXME: check this).