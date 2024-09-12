# 0. About UI Testing
Created Thu Sep 12, 2024 at 12:37 PM

## Components of a UI testing suite
- Runner - structure tests in nested blocks, run them.
- Coverage - Build charts and track how much of the code is covered by the tests.
- Assertions - Comparators for output vs. ideal output, used to verify that the actual results match expected results.
- Domain assertions - assertion utils relevant to the domain.
- Mocks - ability to mock functions, code, API calls. Useful since real calls can be expensive/inefficient. Also used to check various scenarios.
- Snapshots - capture the rendered output or the component's state at a specific moment in time, and store it as a "snapshot". Later tests compare the current output with the saved snapshot to detect unintended changes in the UI or logic. This helps ensure that the UI hasn't changed unexpectedly over time.
- Simulated environment - like a headless browser.

Vitest provides everything except a simulated environment and domain assertions. For these we use happy-dom and RTL respectively.