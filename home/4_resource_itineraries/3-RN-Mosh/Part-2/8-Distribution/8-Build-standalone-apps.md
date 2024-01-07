# 8. Build standalone apps
Created Sat Dec 30, 2023 at 1:57 PM

## Sharing is hard
Expo URL is not a cool way to share your app with non-dev folks, since they'll need to install Expo app, and may find it hard.

A better way is to provide an APK.


## Types of standalone apps
There are two kinds of standalone apps:
1. Bundles for stores - PlayStore/AppStore
2. Build APK for direct install


## Expo's build service
Expo provides a free service where we just run a command and expo generates the bundle.

Note:
- This command can be run only in the 'managed' worfklow option of expo. In the 'bare' workflow, the process is tedious and requires effort.
- Mac not needed - the service runs on the cloud, by default. So you can generate ios bundle without needing a mac.