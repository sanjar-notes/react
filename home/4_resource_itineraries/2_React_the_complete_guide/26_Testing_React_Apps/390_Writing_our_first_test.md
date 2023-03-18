# 390. Writing our first test
Created Wednesday 4 January 2023

Advice: It's a good practice to write tests as close as possible to the actual code. Example - write tests for a button component in it's own file, instead of testing it in an integration/E2E/app wide test.

## How (constructs and intent)
### Jest
- **`test()`** - basic testing unit where assertions are done. aka "test"
- **`expect()`** - used for assertion.
- **`describe()`** - nesting construct. aka "test suite". Not for asserting.
 
### RTL (React Testing Library)
- **`render()`** - renders components, virtually of course.
- **`screen()`** - current state of the virtually rendered UI.
- Inspectors are functions that grab elements from the virtual UI. They are of 3 types:
	- **`get*`** - get an element immediately. throws an error on not found. Maid - immediately get. Use - check existence. Example - `getByText`, `getAllByText`.
	- **`query*`** - same as `*get` except it doesn't throw an error on not found. Maid - ask politely. Use - check nonexistence.
	- **`find*`** - get element asynchronously (i.e. poll the UI until element is found), returns a promise for on found/not-found. Maid - go on a quest. Use - check eventual existence/nonexistence, e.g. list appears only when API call succeeds.


## What (details)
### Jest
No need to import, as these are globally auto-loaded (thanks to `setupTests.js`).
 - **`test`**
	 - Syntax - `test('some text', assertionCallback)`. 
		```jsx
		import HomePage from './some_path';
		test('shows text hello on home page', () => {
			// Arrange
		
			// Act
		
			// Assert, the focus of `test`
		});
		```
	- Default pass - A test with no assertions "passes" by default.
		```jsx
		test('some text here', () => {}); // pass

		// still, need to have both arguments.
		test(); // fail
		test('some text here'); // fail
		```
 - **`expect`**
	 - Syntax - `expect(realValue).myMatcherHere(idealValue)`. 
	 - Argument may be of any type - a JS variable or UI element. 
	 - A matcher may have no argument.
	 - Negative/complement  - `expect(realValue).not.myMatcherHere(idealValue)` for complement. Example:
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
- **`describe`**
	- Syntax - `describe('text here', callbackFunc)`
	- Default pass - A suite with no assertions "passes" by default.
		```jsx
		describe('some text here', () => {}); // pass


		// still, need to have both arguments.
		describe(); // fail
		describe('some text here'); // fail
		```


### RTL (React Testing Library)
These need to be imported in each test file.
- **`render`** - `render(<ComponentOrEquivalentJSX />)`. Non default import from `@testing-library/react`.
- **`screen`** - `screen.inspectorFunc()`. Non default import from `@testing-library/react`.
- About inspectors:
	- All inspectors have two modes -  return a single or multiple elements (as an array). e.g. `getByText` returns a single element, whereas `getAllByText` returns an array of elements. 
	- RTL will through an error if `getByText` is used and there are multiple matches.
	- `*ByText`'s non-strict inspection - `*ByText` takes an object as second argument where we can specify if we want to do an `exact` match or not. e.g. `getByText('hello', {exact: false})`. The default is `exact:true`.