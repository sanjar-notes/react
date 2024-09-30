# 46. Testing with MSW
Created Mon Sep 30, 2024 at 10:09 PM

## Basics
For tests, we don't need to do anything special, having [msw-setup.js](45-MSW-Handlers.md#Handler) file will automatically override `fetch`.
```jsx
import { render, screen } from "@testing-library/react";
import { Users } from "./users"; // assume. Renders list item of users

describe("users", () => {
	test("renders correctly", async () => {
		render(<Users />);

		const users = await screen.findAllByRole("listItem");
		expect(users).toHaveLength(3);
	});
});
```