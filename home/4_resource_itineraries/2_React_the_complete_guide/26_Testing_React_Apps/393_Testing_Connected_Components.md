# 393. Testing Connected Components
Created Sunday 8 January 2023

I use a wrapper component inside `Greetings`, the current custom component.

BUT, the tests still pass. The reason is that RTL still creates virtual UI for the whole component (that we're testing and `RTL.render`ing) tree (FIXME: I think it still keeps "label" that various subtrees are a different component). Simply said, the virtual UI is made for the whole app tree up-to the leaves (HTML elements). So, we don't need to change our tests, in this case, as the content remained the same.

Technically, this is fine. But one should test stuff near the actual code, as much as possible.

Here, the wrapper was not a very heavy - UI wise, state wise or interaction wise, so it's fine.

[Code](https://github.com/exemplar-codes/testing-react-apps-first-tutorial/commit/66bd9b82fef058091af10c7b998914a7e9f1d5b8)

FIXME:
1. How to inspect at the component level, instead of text, role or some other native HTML way? Is it even possible with RTL? If yes/no, why?
2. For testing a small change in a very big UI tree (since RTL renders the whole component tree by default), how to limit rendering children UI nodes, for performance and mocking that might be needed by descendants, the latter being more problematic, as it's not just about performance which could be ignored for once.