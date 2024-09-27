# Misc
Created Tue Sep 17, 2024 at 2:59 PM

## MSW - API mocking
https://mswjs.io/ is an API mocking library that allows you to write client-agnostic mocks and reuse them across any frameworks, tools, and environments.

- Supports REST and GraphQL
- Supports both browser and Node.
- Mocking as a standalone layer - since the interception happens at a worker level, no client side code changes need to be made. And it works everywhere.
- Mock vs Network behavior - using MSW you specify behavior of the network as opposed to ad-hoc mocking. Network behavior is a contract-like description of the network’s expected state, this is the level of abstraction MSW usage will be at.
- Follows [WHATWG Fetch API specification](https://fetch.spec.whatwg.org/) and [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers) spec.

```js
import { setupServer } from "msw/node";
import { http, HttpResponse } from "msw";

// handlers
export const handlers = [
  // Intercept "GET https://example.com/user" requests...
  http.get("https://example.com/user", () => {
    // ...and respond to them using this JSON response.
    return HttpResponse.json({
      id: "c7b3d8e0-5e0b-4b0f-8b3a-3b9f4b3d3b3d",
      firstName: "John",
      lastName: "Maverick",
    });
  }),
];

// server - will override global `fetch`
const server = setupServer(...handlers);
server.listen();

// This is a simple Node.js application that
// does a network request and prints the response.
async function app() {
  const response = await fetch("https://example.com/user");
  const user = await response.json();
  console.log(user);

  // unhandled requests go through by default - with a warning
  const response2 = await fetch("https://api.github.com/users/sanjarcode");
  const user2 = await response2.json();
  console.log(user2);
}

app();
```

## How to test localhost React without hardcoded link
TBD
- One simple trick is simply doing `page.goto("http://localhost:5173")`

## API mocking
- Need to mock because staging is slow.
- Store responses for all APIs and their params/filters. "Very complex".
  - How will update? Run the test suite with Real APIs, store those results, and use them for fast tests.

## Q: Effort to migrate puppeteer <-> playwright?
Not too hard. Syntactic changes mostly.
https://playwright.dev/docs/puppeteer#migration-principles