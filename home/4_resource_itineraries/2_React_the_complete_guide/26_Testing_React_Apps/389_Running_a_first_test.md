# 389. Running a first test
Created Wednesday 4 January 2023

Let's start with a fresh React app bootstrapped using `create-react-app`. [Link](git@github.com:exemplar-codes/testing-react-apps-first-tutorial.git)

1. **Basic setup** - `setupTests.js` does some basic setup - import needed packages.
2. **Test files** - The convention is to the name the test file the same as code file, but with a `.test.js*` extension. Example - `Button.jsx`'s test file should be named `Button.test.jsx`.
3. **Basic pattern of a test** - Write the test, steps being - *Arrange* (simulate), *Act*(do something, like mimick events), *Assert* (inspect and assert).
```js
import { render, screen } from "@testing-library/react";
import App from "./App";

test("renders learn react link", () => {
  render(<App />); // simulate

  // do something - mimick events

  const linkElement = screen.getByText(/learn react/i); // inspect

  expect(linkElement).toBeInTheDocument(); // assert
});
```
4. **Running the test(s)** - Run all tests using `npm test`, this will run all `.test.js*` files. It generates a report - successes/failures/errors. For selected file(s) pass the path/pattern.

![](../../../../assets/Pasted%20image%2020230105000615.png)