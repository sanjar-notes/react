# 35. User Interactions
Created Mon Sep 30, 2024 at 3:45 PM

## `user-event`
[Library link](https://www.npmjs.com/package/@testing-library/user-event)

`user-event` is a package used with RTL used to simulate user events.
RTL also has `fireEvent`. 

But `user-event` is does more "full" interactions than `fireEvent`, and should be preferred. `fireEvent` just triggers one event, while `user-event` triggers more events (mimicking how real events trigger more helper events).

## Installation
You need to install it separately `npm i -D @testing-library/user-event`. CHECK: or do you?

## All functions
https://testing-library.com/docs/user-event/v13/

## Tech
- The UI layer and trusted events are not programmatically available.

## Types of interaction APIs
- [Pointer](https://testing-library.com/docs/user-event/pointer#selectiontarget) - allows to simulate interactions with pointer devices. Low level.
- [Keyboard](https://testing-library.com/docs/user-event/keyboard) - allows to simulate interactions with a keyboard. Low level.
<br />

- [Clipboard](https://testing-library.com/docs/user-event/clipboard) - enable testing of workflows involving the clipboard
- [Utility](https://testing-library.com/docs/user-event/utility) - don't have one-to-one equivalents in a real user interaction. High level.
- [Convenience](https://testing-library.com/docs/user-event/convenience) - shortcuts - so you don't have to use lower level APIs. High level.