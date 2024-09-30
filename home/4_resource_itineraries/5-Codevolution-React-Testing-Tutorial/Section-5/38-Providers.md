# 38. Providers
Created Mon Sep 30, 2024 at 5:21 PM

## Why
In React, the app tree is generally wrapper by Providers, like Redux, Toast, Routing etc.

And these providers are required for proper rendering of the components, i.e. you can't test components in isolations, atleast for integration tests (sometimes even unit tests require providers).
```jsx
// assume MuiMode, a heading that prints 'dark mode' or 'light mode' as per config
// assume AppProviders, a helper component that wraps various Providers, in this case MUI
test("renders text correctly", () => {
	render(<MuiMode />); // would fail, needs AppProviders
	render(<MuiMode />, { wrapper: AppProviders }); // works now

	const headingElement = screen.getByRole("heading");
	expect(headingElement).toHaveTextContent("dark mode");
});
```

But the problem with using `wrapper` config is that it needs to be set for each test case.
It would have been better if we could specify the wrapper at some global config, reducing the code for each test.

Note:
-  The `wrapper` option might seem like a useless option, one could have wrapped the provider in the render itself. CHECK: is this really redundant.