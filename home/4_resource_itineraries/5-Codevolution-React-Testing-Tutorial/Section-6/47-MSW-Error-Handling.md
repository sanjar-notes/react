# 47. MSW Error Handling
Created Mon Sep 30, 2024 at 10:16 PM

## Dynamic/local handlers
Sometimes, we need routes that are used only by a small number of tests, or we need a special response for a already added handler.

Handling these scenarios is simple, all we need to do this attach+override a handler, which can be easily done by mutating the `server` singleton that we created in [msw-setup.js](45-MSW-Handlers.md#Handler)

Example - we want to test for an APIs failure. Having a fail handler globally is not good, since only test uses this.
```jsx
import { server } from "./msw-setup";
import { rest } from 'msw';

describe("users", () => {
	test("renders correctly", async () => {
		const localHandler = rest.get("https://jsonplaceholder.typicode.com/users"), (req, res, ctx) => {
			return res(ctx.status(500));
		};
		
		server.use(localhandler);
		render(<Users />);

		const errorText = await findByText("Error fetching users");
		expect(errorText).toBeInTheDocument();
	});
});
```

## Residue?
Will using this local handler cause the global handlers to be polluted?
No, since we run `afterEach(() => server.resetHandlers())` in the [msw-setup.js](45-MSW-Handlers.md#Handler), so handlers are reset for each test. We're good.