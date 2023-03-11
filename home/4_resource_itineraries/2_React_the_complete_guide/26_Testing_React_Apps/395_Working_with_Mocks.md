# 395. Working with Mocks
Created Sunday 8 January 2023

## Why/Situation
This is still not ideal:
1. **Events not time** - working with hardcoded wait times, or with time instead of events is not good practice.
2. **Network requests** - test suites should not contact the outside world, like at all.
3. **Infrastructure cost** - if the test makes actual changes, e.g. making requests, mutating databases, cache, filesystems and other stuff, one has to maintain infrastructure just even for routine automated testing. This is not practical, especially since modern CI/CD pipelines run all tests for before each deployment.
4. **DX** - if the test suite makes real network calls, every developer will need a powerful internet connection to work, which will be big pain, coz 
	   1. Waiting
	   2. Very high internet bill.
	   3. Need for overpowered laptops. 


## How
There are two solutions:
1. Mock external resources, as much as possible, at the client side itself. Problem - mocking is a client side responsibility.
2. Have a dedicated testing server, that does the mocking. Less client side test code. Problem - dedicated server cost.

Here (for this course), we'll mock everything on the client side itself, i.e. we'll to mock network calls only, since this is a React focused course.

A simple way is to built in code, like `fetch`, `localStorage` etc. This paradigm is supported by Jest. Simply said, we override parts of the `window` object itself, e.g. `window.fetch`.

Obvious point - We want to test only the code we wrote, not other things - e.g. there's no need to test browser's `fetch` function, because it's assumed to be OK. Maybe the point Max was trying to make was that we should mock as little as possible - only parts that we are using in our app code.


## What
- For mocking functions, use `jest.fn()` - it returns a function. It's better to use this than have a normal custom function, since `jest.fn()` has additional properties.
- We are using the `mockResolvedValueOnce` property that is used to mock an async function. Example:
```jsx
test("renders posts if request succeeds - mocked", async () => {
    window.fetch = jest.fn();
    window.fetch.mockResolvedValueOnce({
      json: async () => [
        {
          userId: 1,
          id: 1,
          title:
            "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
          body: "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto",
        },
      ],
    }); // Keep mock consistent -  fetch returns an object than has an async function called `json`.

    render(<MyAsyncComponent />);

    const listItems = await screen.findAllByRole("listitem");

    expect(listItems).not.toHaveLength(0);
  });
```
[Code](https://github.com/exemplar-codes/testing-react-apps-first-tutorial/tree/03c9b723f867a32dcdf917db6000707e1cdee466)