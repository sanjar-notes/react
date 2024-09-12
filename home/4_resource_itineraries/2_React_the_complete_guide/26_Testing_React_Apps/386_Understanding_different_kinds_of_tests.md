# 386. Understanding different kinds of tests
Created Wednesday 4 January 2023

Tests in software development, including automated tests, can be classified on various parameters.

Here, we're talking about **automated tests** only.

## Types of automated tests
Based on scope/scale of the test.

| Name        | Scope                                                           | Typical count | Importance     | Effort needed |
| ----------- | --------------------------------------------------------------- | ------------- | -------------- | ------------- |
| Unit        | individual building blocks tested in isolation                  | 100s - 1000s  | Most important | Less          |
| Integration | combination of building blocks (that interact or work together) | 10s           | Important      | High          |
| End-to-End  | complete flow, or the whole app itself.                         | < 10          | Less important      | Very high     |

Note: the 3 terms are loosely defined.

### 1. Unit tests (details)
These tests test the smallest possible building blocks. Examples - functions, UI components like buttons, i18n text components, that are used at many places.

They are considered to be the most important - based on the general assumption that if small parts are fine, the larger parts will also be OK.

### 2. Integration tests (details)
Here, we test a combination of multiple building blocks. Example - a page that has both a table and a search box, to test if the search functionality updates the table properly.

### 3. End-to-End tests (details)
Here, we test a complete app flow or a large feature. They take a lot of effort to write, and can require updates over time. 

They are important, but can also be done manually (partially).

If a feature is large and complex but doesn't have a lot of possible combinations, it may be better to just do manual testing.