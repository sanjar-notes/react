# 12. Storing user actions when offline
Created Sat Dec 30, 2023 at 1:55 PM

We cached data as a 'offline' strategy. But more can done - we can store user actions.

Implementing this quite hard, since we'll need to do:
1. Handle optimistic updates
2. Conflict resolution
3. Retry actions when network is back
4. Check if a feature flow should be usable in offline mode or not

## Practically
Practically, some sort of library or SDK is used for this. Example:
1. Firebase
2. Realm - maintains an offline on device database for us.

## YAGNI
Do you really need offline user action support?