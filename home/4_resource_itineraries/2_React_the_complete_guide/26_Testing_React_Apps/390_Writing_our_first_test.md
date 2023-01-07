# 390. Writing our first test
Created Wednesday 4 January 2023

Advice: It's a good practice to write tests as close as possible to the actual code. Example - write tests for a button component in it's own file, instead of testing it in an integration/E2E/app wide test.

## How
### Jest
- `test()` - basic testing unit where assertions are done.
- `expect()` - used for assertion.
- `describe()` - nesting construct.
 
### RTL (React Testing Library)
- `render()` - renders components, virtually of course.
- `screen()` - current state of the virtually rendered UI.
- Inspectors are functions that grab elements from the virtual UI. They are of 3 types:
	- `get*` - throws an error on not found. Maid - immediately get. Use - check existence.
	- `query*` - doesn't throw an error on not found. Maid - ask politely. Use - check nonexistence.
	- `find*` - returns a promise for on found/found. Maid - go on a quest. Use - check eventual existence/nonexistence.


## What (details)
### Jest
No need to import, as these are globally auto-loaded (thanks to `setupTests.js`).
 - `test` - `test('some text', assertionCallback)`
```jsx
import HomePage from './some_path';
test('shows text hello on home page', () => {
	// Arrange

	// Act

	// Assert, the focus of `test`
});
```
 - `expect` - `expect(realValue).myMatcherHere(idealValue)`. Matcher may or may not need an argument. Also `expect(realValue).not.myMatcherHere(idealValue)` for complement. Value can be anything - a JS variable or UI element. Example:
```jsx
// assert presence/existence
// const helloElement = screen.getByText('Hello World!'); throws error
const helloElement = screen.getByText('Hello World!');
expect(helloElement).toBeInTheDocument();

// assert absence
// const helloElement = screen.getByText('Hello World!'); throws error
const byeElement = screen.queryByText('Bye World!');
expect(byeElement).not.toBeInTheDocument();
```
- `describe` - nesting construct. Not for asserting.
```jsx
describe('some text here', () => {

	test();

	describe();
});
```

### RTL (React Testing Library)
These need to be imported in each test file.
- `render` - `render(<ComponentOrEquivalentJSX />)`. Non default import from `@testing-library/react`.
- `screen` - `screen.inspectorFunc()`. Non default import from `@testing-library/react`.
- To use a complement for a matcher - use them from inside `not` attribute.