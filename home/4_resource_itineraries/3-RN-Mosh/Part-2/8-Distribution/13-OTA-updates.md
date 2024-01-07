# 13. OTA updates
Created Sat Dec 30, 2023 at 1:57 PM

## What, how and advantage
Expo OTA updates are a super power.

The story is, that native apps on Apple or ANdroid, built with Kotlin/Swift need to the build + distribute process whenever they are updated.

But RN doesn't have to, since it's JS. So on both iOS and Android, OTA updates are allowed.

So, we don't have to go through build + distribute steps for updates. It happens automatically, i.e. whenever we update the app code, and trigger a build, the updated bundle gets saved to Expo cloud. Now, all expo managed apps running on user devices do a update check with Expo server when they start, and if found, download the update in the background, to be used on next start of the app.


## When to use OTA updates
If update involves:
- Assets like images
- Changes in text
- Bug fixes
- Small features

## When not to use OTA updates
Large features can be done in OTA mode too, but it's generally better to do the build + distribute step for them, and also update store level description, screenshots etc.


## Workflow matters? no.
OTA updates are supported in both Expo 'managed' and 'bare' workflows.