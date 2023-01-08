# 394. Testing Asynchronous Code
Created Sunday 8 January 2023

### A note about inspectors
- `*byText`, which gets us a UI element containing the text.
-  `*byRole`, to inspect by tag. But it doesn't work with tag names directly, it uses "roles" - [MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques#states_and_properties), [W3C](https://www.w3.org/TR/html-aria/#docconformance).
FIXME: Why does RTL have a `byTagName`? [this](https://github.com/testing-library/react-testing-library/issues/853) is not very convincing. Find out.

## Why
Why do we need to talk about async testing separately. Simply because `get*` and `query*` inspectors try to find the element instantly(soon as the virtual UI is ready). But elements dependent on async ops don't appear instantly.


## How (async inspection works)
There's a delay/wait before the async UI elements (i.e. dependent on async ops) appear.

There are two (similar) ways to do inspection here:
1. **Wait and check once** - Wait until a given time and check once.
2. **Poll until a max time** - we poll the virtual UI until a max time bound.

They are essentially the same, \#1 is the worst case scenario of \#2.


## What
RTL's `find*` inspector polls the virtual UI, until a fixed time bound (1 second by default).

We can also manage the waiting/poll-bound time, [like so](https://github.com/exemplar-codes/testing-react-apps-first-tutorial/tree/b05bd19911e230a97a4570961dd664bee2636c2b) :
```js
const listItems = await screen.findAllByRole(
      "listitem",
      {
        /** exact etc */
      },
      {
        /* wait options - default wait time is 1 second, can be changed */
      }
    ); // re-inspects virtual UI for specified wait conditions
```