# 393. Testing Connected Components
Created Sunday 8 January 2023

I use a wrapper component inside `Greetings`, the current custom component.

BUT, the tests still pass. The reason is that RTL still creates virtual UI for the whole tree (FIXME: I think it still keeps "label" that various subtrees are a different component). Simply said, the virtual UI is made for the whole app tree up-to the leaves (HTML elements). So, we don't need to change our tests, in this case, as the content remained the same.

Technically, this is fine. But one should test stuff near the actual code, as much as possible.

Here, the wrapper was not a very heavy - UI wise, state wise or interaction wise, so it's fine.

[Code](https://github.com/exemplar-codes/testing-react-apps-first-tutorial/commit/3fe21068240eb32e784ede688229b11092704198)