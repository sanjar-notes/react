# 9. Build the ios app
Created Sat Dec 30, 2023 at 1:57 PM

## Step 1 - Register with Apple
To add an ios app to the App store, you need to register in the Apple Developer Program.
You can sign up as an individual or an organization. Need to upload some document like drivers license.

This involves a fee of around 100 dollars. Renewal fee is 100 year, per year.
If you don't won't be updating the app anytime soon, renewal is not needed. The latest version of the app will always be available on the AppStore.


## Step 2 - Configs - register new app metadata
Configs. Go to app.json
- `ios.supportsTablet` - true or false
- `ios.bundleIdentifier` - "com.sanjarcode.donewithit". Should be unique to the app, and usually never changes. This is called reverse DNS notation. Of course, there's no need to create a website or something named like so.
- `ios.buildNumber` - "1.0.0", update this when you build a new bundle
- `version` - version as it will appear in app metadata on the store, and after installation

Note: you may get "build already exists". This usually means you forgot to bump up the build number.


## Step 3 - generate the bundle
Run `expo build:ios`. Then answer the prompts:
1. yes I have apple account
2. apple id
3. password
4. 'Getting Distribution Certificates on Apple Servers'. Choose "let expo handle"
5. 'Provide Apple PNS key'. Choose "let expo handle"

The prompt will now show a URL and go into loading state. Press Ctrl + C, no issues, build won't be aborted. Click the URL to check build progress.

![](/assets/9-Build-the-ios-app-image-1-a30d4072.png)

Note:
- Large bundle size - even small Expo apps are large, like ~50 MB. This happens because Expo bundles a lot of functionality by default, even if the code doesn't use it. There's been some effort from Expo to reduce this bloat.
- If large size is not ok for you. There's no choice but to eject from Expo. But do this only if you know how to build ios apps on your own.