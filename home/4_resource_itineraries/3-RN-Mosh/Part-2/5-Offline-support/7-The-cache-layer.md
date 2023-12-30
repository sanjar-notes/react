# 7. The cache layer
Created Sat Dec 30, 2023 at 1:55 PM

If the fetched data has complex relations, SQLite method is preferred.

Else if data is simple and non-sensitive, we use AsyncStorage. For sensitive  data, use SecureStorage.

## Wrapper - migration
We'll use AsyncStorage for caching (including for offline support).
But we shouldn't use it directly. Maybe our data is termed sensitive by some regulation or we want to migrate to some other library/solution, this would be very hard to do if our code directly use the AsyncStorage library and its functions.

The fix is simple. We need to come up and define functionality we need from the library, and create a wrapper for around the library. This way, only the wrapper interacts with the library code. And our app code uses the wrapper. Future migration wise, we'd need to change only one file.

## Wrapper - caching need
A thin wrapper won't do in our case, since we need to label our data with timestamps.

Now, adding timestamps to data as part of feature/app code would be cumbersome and error-prone. So we should automate it.

So we'll add these functionality in the wrapper:
1. Auto-label stuff when we "add" stuff to the async storage via the wrapper.
2. Serialize-deserialize data as AsyncStorage can only deal with strings
3. Auto remove expired things