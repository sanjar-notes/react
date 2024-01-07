# 7. Expo publish
Created Sat Dec 30, 2023 at 1:57 PM

Expo publish is a quick and simple way to share out app with out team or anyone with the Expo Go app installed on their phone.

After publishing, you get a URL that can be shared.

Command for publishing is:
```sh
npx expo publish -release-channel='myStaging' ## old
```

Sharing can be done in URL only or private mode too.

This is done by having "privacy" key in app.json
- By default - value is `unlisted`, this hides the URL from search engines.
- `public` - makes the URL searchable and accessible to all
- `private` - also supported TBD


## EAS - the new way
Expo publish has been "sunset" in 2024, last day is Feb 2024. See [official blog](https://blog.expo.dev/sunsetting-expo-publish-and-classic-updates-6cb9cd295378).
It's now called 'Classic Updates'. The new way to build/publish is called 'EAS Update'.

Classic Update will still remain available for SDK 49 or earlier.

[Migration guide - expo-publish to eas](https://docs.expo.dev/eas-update/migrate-from-classic-updates/)