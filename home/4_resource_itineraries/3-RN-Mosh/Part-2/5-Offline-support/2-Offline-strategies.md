# 2. Offline strategies
Created Sat Dec 30, 2023 at 1:55 PM

Strategies for building offline capable apps:
1. Notify the user
2. DIsable certain features
3. Cache-data
4. Store user-actions, to be run when connection is back.

btw, Each of these strategies can mostly be applied independently.

## YAGNI and cost
Do you really need sophisticated offline strategies?
A simple detect message won't do?

The strategies discussed above vary in effort and complexity according from app to app. But they definitely need more effort than building a happy-path app. Answer this question before implementing.