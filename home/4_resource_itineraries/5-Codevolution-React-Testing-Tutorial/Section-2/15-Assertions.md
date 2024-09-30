# 15. Assertions
Created Fri Sep 27, 2024 at 5:32 PM

An assertion is a value checker. `expect` from the runner is one.
Assertions always work with a matcher, like `.toBeInTheDocument`.

We need to use `@testing-library/jest-dom` to get UI specific matchers. Install this, and import `@testing-library/jest-dom/vitest` in your vitest setup file.

## Structure of an assertion
`assertion(value).matcher()`

e.g. `expect(textElement).toBeInTheDocument()`