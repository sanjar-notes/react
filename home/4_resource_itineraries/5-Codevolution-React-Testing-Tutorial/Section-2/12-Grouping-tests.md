# 12. Grouping tests
Created Fri Sep 27, 2024 at 5:37 PM

- `describe` blocks can be nested without limits.
- `test` and `it` are aliases.
	- `test` has some variations, `test.skip`, `test.only`, `test.skipIf(boolean)()`, `test.runIf(boolean)()`
	- `test.each` - https://vitest.dev/api/#test-each. Run the same test against different args.