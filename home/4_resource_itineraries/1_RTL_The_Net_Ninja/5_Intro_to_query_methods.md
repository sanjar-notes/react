# 5. Intro to query methods

### Why
Query methods are used for locating subcomponents/elements of a component.

##### Types of query methods (prefixes)
| Type of Query | 0 Matches | 1 Match | &gt;1 Matches | Retry (Async/Await) |
| ------------- | --------- | ------- | ------------- | ------------------- |
| `getBy`       | error     | element | error         | No                  |
| `queryBy`     | `null`    | element | error         | No                  |
| `findBy`      | error     | element | error         | Yes                 |
| `getAllBy`    | error     | array   | array         | No                  |
| `queryAllBy`  | `[]`      | array   | array         | No                  |
| `findAllBy`   | error     | array   | array         | Yes                 |
- `queryBy` is meant to assert non-existence.