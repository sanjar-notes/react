---
tags:
  - slow-connection
  - loader
  - ActivityIndicator
  - RN-core
  - throttling
  - network
---
# 2. Slow connection and loader
Created Sat Dec 30, 2023 at 1:55 PM

Always test the app on slow internet - both speed and latency wise. One simple way is via the react-native-debugger (that we installed previously); it has the standard network throttling features like browser network tab.

Also, the `<ActivityIndicator animating={isFetching} size={48} />` is a built-in loader component.