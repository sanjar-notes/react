# 391. Grouping tests together with test suites
Created Thursday 5 January 2023

## Why
Testing suites are a way to organize tests in a codebase into logical units - e.g. all tests for a feature/component/cases.


## How
- Nesting, as usual. 
- Multiple files. Keep tests isolated and close to their actual code, as much as possible.


## What
The `describe` function is used to create test suites.
Example:
```js
describe('Greeting component', () => {
	test('renders Hello World! text', () => {
		const helloElement = screen.getByText('Hello World!');
		expect(helloElement).toBeInTheDocument();
	});
})

describe('Greeting component', () => {
	test('renders Hello World! text', () => {
		const helloElement = screen.getByText('Hello World!');
		expect(helloElement).toBeInTheDocument();
	});

	test('renders Hello World! text', () => {
		const helloElement = screen.getByText('Hello World!');
		expect(helloElement).toBeInTheDocument();
	});
})
```
Rules
1. Both suites/tests can have setup code.
2. Only a test can do assertions.
Nesting:
1. A file can have any number of suites/tests.
2. A test cannot have suite/test.
3. A suite can have `test`s or other suites.

**Simply said**, suites are meant to be containers, whereas tests are meant for assertions. That's the intent, but both are allowed to do any other computation like render, inspect.