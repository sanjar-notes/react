# 4. Caching
Created Sat Dec 30, 2023 at 1:55 PM

Caching is more important in mobile apps, since they may be operating on slow cellular connections and battery usage is important.

Caching strategy, in the simplest way for mobile apps, focuses on "retaining sucessfully fetched data".
It does *not care* about mutations/actions the user does.

If this strategy is being used in isolation, action UIs should be disabled. This will *prevent* a variety of errors and unfruitful fixes for them.

## Storage?
Tech wise, there are 3 ways to implement caching in an RN app:
1. [AsyncStorage](https://www.npmjs.com/package/@react-native-async-storage/async-storage) - a cross platform library for storing string key value pairs. Not encrypted and has limit of 6MB. Not meant for sensitive data. The RN analogue of browser's localStorage.
2. [SecureStore](https://docs.expo.dev/versions/latest/sdk/securestore/) - key value store. Is encrypted. Limit of 2MB. Developed for Expo. RNCLU alternatives also exist.
3. [SQLite](https://docs.expo.dev/versions/latest/sdk/sqlite/) - large store. Good if you're OK writing SQL. Unencrypted. Useful if stored data has complex relations

Note: in all these methods, data is persisted across restarts, which is what we need. Gets trashed on uninstall, but fine.