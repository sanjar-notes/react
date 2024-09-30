# 2. RTL
Created Thu Sep 12, 2024 at 12:31 PM

[RTL](https://testing-library.com/) is short for React-Testing-Library. Its a UI focused assertion library/UI testing library.
## Problem
- You want tests for your UI that avoid including implementation details and rather focus on making your tests give you the confidence for which they are intended.
- You want your tests to be maintainable so refactors (changes to implementation but not functionality) don't break your tests and slow you and your team down.

RTL solves these issues by providing a library that has relevant functions (matchers) for UI testing, including framework specific methods for React, Angular.

## What RTL is not
It is:
- not a test runner or framework
- not specific to a testing framework
- not specific to an app framework - i.e. works for vanilla, React, React Native, Angular etc.
- Does not include an environment
- Provides native DOM nodes and not framework 'components', to work with.

So you would need 2 extra things - a framework and a environment, in order to use RTL.'

## Features
- Simple API
- React matchers
- Unit, integration and end-to-end tests can be written.
- DOM only no components - Does not provide access to rendered components methods and instances, only DOM nodes.
- Browser extension is available
- Eslint plugins
- Works with React Native too

## Philosophy
- Tests should resemble the way your software is used, as if a real person was using it.
- You test behavior and not implementation details.
- If rendering components (framework), then you should deal with DOM nodes instead of component instances.

See https://kentcdodds.com/blog/testing-implementation-details
## RTL with Vite ?
Works fine.

Some points
- `@testing-library/jest-dom` is not needed. Vitest already has it.
- Linters for React Testing Library.
	- [eslint-plugin-testing-library](https://github.com/testing-library/eslint-plugin-testing-library). [Config](https://github.com/testing-library/eslint-plugin-testing-library?tab=readme-ov-file#eslint-overrides)
	- [eslint-plugin-jest-dom](https://github.com/testing-library/eslint-plugin-jest-dom). [Config](https://github.com/testing-library/eslint-plugin-jest-dom?tab=readme-ov-file#recommended-configuration)
	- Make sure you lint only test files with these packages, so add them as glob override.

## Reading - Testing library
- [x] Getting started
- [x] Guiding principles
- [x] FAQ
- [ ] Core API
	- [x] Queries
		- [x] About Queries
		- [ ] Specific info
	- [ ] User actions
		- [x] Firing events - `user-event` should be preferred over `fireEvent`.
		- [x] Async methods
		- [x] Appearance/dis - queryByText, toBeInTheDocument
		- [x] Considerations for fireEvents - using fireEvents is fine practically, focus-blur testing is possible.
		- [ ] Fake timers - important 2-step process to flush timers
	- [ ] Advanced
		- [x] Accessibility
		- [x] Custom queries - easily possible
		- [x] Debugging
		- [x] Querying within elements - [within](https://testing-library.com/docs/dom-testing-library/api-within)
		- [ ] Configuration options
	- [x] Frameworks
		- For Vite, no need to install jsdom, just specify.
		- [x] DOM testing - [Cheatsheet](https://testing-library.com/docs/dom-testing-library/cheatsheet)
		- [x] React Testing library
	- [x] User interactions
	- [x] Ecosystem

## Reading - RTL
- [Installation](https://testing-library.com/docs/react-testing-library/intro)
- [The problem](https://testing-library.com/docs/react-testing-library/intro#the-problem)
- [The solution](https://testing-library.com/docs/react-testing-library/intro#this-solution) - Provides utils on top of [react-dom and react-dom/test-utils](https://testing-library.com/docs/react-testing-library/intro#this-solution)
	- Find nodes by text or `data-testid`
- [Example](https://testing-library.com/docs/react-testing-library/example-intro)
- Setup
	- [Custom](https://testing-library.com/docs/react-testing-library/setup#custom-render) `render` method is helpful - that includes global store/context Providers. Re-export everything, so all imports are from this custom util file and not directly from RTL.
	- [Add alias](https://testing-library.com/docs/react-testing-library/setup#configuring-jest-with-test-utils) for the test-util file so relative imports are not needed.
- [Cheatsheet](https://testing-library.com/docs/react-testing-library/cheatsheet)
- [User event setup](https://testing-library.com/docs/user-event/setup)


## Articles
- [Vitest with React Testing Library](https://www.robinwieruch.de/vitest-react-testing-library)