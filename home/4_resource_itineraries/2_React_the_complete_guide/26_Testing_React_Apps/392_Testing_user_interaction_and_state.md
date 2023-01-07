# 392. Testing user interaction and state
Created Saturday 7 January 2023

To test interaction, let's [add](https://github.com/exemplar-codes/testing-react-apps-first-tutorial/commit/4015547edaba1723de41bba4ca255f5c07bcc2a0) some state, for realism.

## Interaction
We can interact using the `userEvent` object available as a default import from the `@testing-library/user-event` package.

It contains many events - click, scroll etc. The syntax for click is `userEvent.click(myButtonElement)`. FIXME: It's a synchronous operation, here atleast, is this always the case. [Code](https://github.com/exemplar-codes/testing-react-apps-first-tutorial/commit/1542ecea9755848f75c31548fb17ac5ae6125d7a).

FIXME: I [can](https://github.com/exemplar-codes/testing-react-apps-first-tutorial/commit/08c221f7cc39d93f8f82045a80bfc23861cc60d6) click the element directly, just like vanilla JS.
1. Is this discouraged?
2. How is it different from `userEvent`?
3. Potentially direct actions (like scroll, keyboard) - direct in the sense that they are not focused for a particular element seems easier with `userEvent`, but it be done using `document` element as well - what are the differences?

Some observations:
- Test for all possibilities - Taking into account all possibilities that make sense is very important. [Code](https://github.com/exemplar-codes/testing-react-apps-first-tutorial/commit/cb458d36c1966488f202984d9336be3b8b4ed448)
- There may be multiple matchers which could be used interchangeably for a given scenario. [Code](https://github.com/exemplar-codes/testing-react-apps-first-tutorial/commit/3fbd25bd74e10fb8f92e02a3b9a6cfbf68d7200d)
- Use proper (tight) inspectors - when checking for presence, use `get` instead of `query`. Both would give the same result, the `get` is better as it'll raise an error. [Code](https://github.com/exemplar-codes/testing-react-apps-first-tutorial/commit/4ab5948505af3b935d1fbc3cb94c773e063aea34). FIXME: really, why not be silent and not raise errors - the report will mention failure anyway.