# 17. Queries
Created Fri Sep 27, 2024 at 5:51 PM

## 3As
3A - arrange, act, assert.

Every test we write generally involves the following basic steps
1. Render the component
2. Find an element rendered by the component
3. Assert against the element found in step 2 which will pass or fail the test

To render the component, we use the render method from RTL

For assertion, we use expect passing in a value and combine it with a matcher function from jest or jest-dom

## List of queries
[List of queries](https://testing-library.com/docs/react-testing-library/cheatsheet/#queries)
[Query priority](https://testing-library.com/docs/queries/about#priority)


- getBy...
- queryBy...
- findBy...

- getAllBy...
- queryAllBy...
- findAllBy...

## Query suffixes
There are many variations of queries
- role
- labelText
- placeHolderText
- Text
- AltText
- Title
- Testid
