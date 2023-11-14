# 1. Core Components and APIs
Created Tue Nov 14, 2023 at 11:26 PM

## React remains the same
React code - JavaScript, JSX, props, state, hooks all behave as is on all platforms

## RN constructs
RN has 2 fundamental constructs:
1. Core components - `Text`, `View` etc
2. Core APIs - Keyboard, Camera, `Platform`

Just like the web, these two help with making UIs and interacting with the device.

## Context matters
But an important thing to keep in mind in RN is that it's targets multiple platforms, so a construct may be:
1. "Cross-platform" - works the same in all platforms. Example - `View`, `Text`
2. "Platform-specific" - works and behave differently in different platforms.