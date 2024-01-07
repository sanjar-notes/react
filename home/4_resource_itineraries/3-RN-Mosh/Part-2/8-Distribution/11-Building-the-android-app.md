# 11. Building the android app
Created Sat Dec 30, 2023 at 1:57 PM

## Config
Go to app.json and set:
- `android.package` - to a unique string (representing the app) in reverse DNS location. Example: "com.sanjarcode.doneWithIt". This is usually never changed. There's no need to have a website or anything for the value you enter above.
- `android.versionCode` - number. This is not seen by users (`version` key does that). This is used by Google to keep track of build numbers. Bump this up when you submit new builds.

## Do the build
Run `expo buld:android`. Answer prompt
- Build-type. Choose
	- APK - for generating setup file
	- App-bundle - for generating file to be uploaded to PlayStore.
- Key-store - Choose "let expo handle"

The prompt will now show a URL and go into loading state. Press Ctrl + C, no issues, build won't be aborted. Click the URL to check build progress.

On the URL, you'' get to download the .apk or app-bundle (whatever you chose earlier).

Note:
- Large bundle size - even small Expo apps are large, like ~50 MB. This happens because Expo bundles a lot of functionality by default, even if the code doesn't use it. There's been some effort from Expo to reduce this bloat.
- If large size is not ok for you. There's no choice but to eject from Expo. But do this only if you know how to build ios apps on your own.


## Generate the keystore (PlayStore)
Run `expo fetch:android:keystore`. This generates a `.jks` file.
The file is like an authentication key and used to update the app on PlayStore.

So keep it private and safe. If you lose it, we'll need to submit the app as a new app, foregoing the name and unique identifier too.