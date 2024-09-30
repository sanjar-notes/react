# 45. MSW Handlers
Created Mon Sep 30, 2024 at 10:08 PM


`handlers` is an array of endpoints accepted by the `server` expose.

## Handlers setup
```js
// msw-setup.js
import { rest } from 'msw'; // btw, graphQL is also available
import { setupServer } from 'msw/node';

export const handlers = [
  rest.get('https://jsonplaceholder.typicode.com/users', (req, res, ctx) => {
    return res(
      ctx.status(200),
      ctx.json([
        {
          name: 'Bruce Wayne',
        },
        {
          name: 'Clark Kent',
        },
        {
          name: 'Princess Diana',
        },
      ])
    )
  }),
]

export const server = setupServer(...handlers);
```
```js
// setupTests.js
beforeAll(() => server.listen())

// Reset any request handlers that we may add during the tests,
// so they don't affect other tests.
afterEach(() => server.resetHandlers())

// Clean up after the tests are finished.
afterAll(() => server.close())
```

