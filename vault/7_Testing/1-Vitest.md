# 1. Vitest
Created Wed Sep 11, 2024 at 11:24 AM

## Components of a UI testing suite
- Runner - structure tests in nested blocks, run them.
- Coverage - Build charts and track how much of the code is covered by the tests.
- Assertions - Comparators for output vs. ideal output, used to verify that the actual results match expected results.
- Mocks - ability to mock functions, API calls. Since real calls can be expensive/inefficient. Also used to check various scenarios.
- Snapshots - capture the rendered output or the component's state at a specific moment in time, and store it as a "snapshot". Later tests compare the current output with the saved snapshot to detect unintended changes in the UI or logic. This helps ensure that the UI hasn't changed unexpectedly over time.

## Why Vitest
Vite tooling is uniquely fast. So we're switching app tooling to Vite.
For testing, if we use Jest then its two unconnected things to manage - one for Vite and one for Jest. Also Jest is also slow. So we'll use Vitest. Single vite config does both app and test tooling.

## Alternative comparisons
- [Jest](https://vitest.dev/guide/comparisons.html#jest) - setup overhead if already using Vite. Slower. Worse DX.
- [Cypress](https://vitest.dev/guide/comparisons.html#cypress) (headed + headless) - UI testing framework. Cypress is real, Vite is headless. Similar to WebDriverIO. Complementary to Vite if end-to-end tests are also needed.
- [WebDriverIO](https://vitest.dev/guide/comparisons.html#webdriverio) (headed + headless)- better than Cypress in that it uses actual w3c WebDriver standards. Runs on mobile as well.
- [Web Test Runner](https://vitest.dev/guide/comparisons.html#web-test-runner) (headed)
- [uvu](https://vitest.dev/guide/comparisons.html#uvu) - single threaded too slow.

## Vitest vs Jest
[Video](https://youtu.be/adBPXEUhj6Q?si=jcGLh9xLlurulcE9)
- Installation and configs: Vitest runs with Vite with almost no config. Jest needs config.
	- TS enabled by default in Vitest
	- Both app and test config in the same file - vite.config.js
- Performance: Vite + happy-dom is faster.
	- esbuild helps in Vite's case.
	- Re-execute changed file: Vite only runs only dependents, while Jest runs based on git diff and can therefore be worse.
- Dependencies. Vitest (61, 26MB) vs Jest (196, 32MB)
- Imports - describe, it are imported explicitly, so less magic.
- Restorable mocks: All mocks are restorable in Vitest - behavior is reset. Enable test.restoreAllMocks: true in vite.config.js
- Command: by default runs in Watch mode. In CI mode runs in single mode. Jest OTH requires a flag always.
- ESM: ESM support is available by default in Vitest. Jest forces CommonJS in its pipeline, which is not helpful since most libs are ESM now.

See all [features](https://vitest.dev/guide/features.html).


## Vitest setup
[Video](https://youtu.be/7f-71kYhK00?si=6tfKzMtk9IE3oZu6)
- `pnpm i -D vitest`
- Add `"test": "vitest"`
- `--coverage` options shows a report. It prompts to install another package, say OK.
- `test.coverage.reporter` = `text` (console log, defaullt), `html` generates HTML file for the report.
- [Hack](https://vitest.dev/guide/in-source.html) - add tests to the same file, surround test code with `if (import.meta.vitest)`
	- This has a side effect that test code becomes included in `build`. To prevent this, set `viteConfig.define = { "import.meta.vitest", "false" }`, so the bundler gets a hint to ignore test code.

## MSW and UI testing
[Video1](https://youtu.be/Aqz43LVbnTk?si=ynmqfOKRDf1W4aIu)
[Video2](https://youtu.be/FJRuG85tXV0?si=cvRwLPywa10MjF9y)

`msw` is a package recommended by Vite for mocking APIs.

## Reading docs
- [x] Why Vitest
- [x] Getting started
- [x] Features
- [x] Workspace
- [x] CLI
- [x] Test filtering
- [x] Reporters
- [x] Coverage
- [x] Snapshot - interesting point pass/fail(wrong or update) cases. Serialization for HTML, image, ImmutableJS, and React elements.
- [x] [Mocking]()
	- [x] Dates
	- [x] Functions - spying (was called in what ways), and mocking (returning mocked responses)
	- [x] Globals - mock the `_globals` object
	- [x] Modules - mock 3rd party, or own libraries and modules.
		- [x] Automocking by default - empty envelope
		- [x] Virt modules
		- [x] File system (memfs)
		- [x] [API requests](https://vitest.dev/guide/mocking.html#requests) - use MSW, the app code calls API like usual. But calls are intercepted and mocked.
		- [x] [Timers](https://vitest.dev/guide/mocking.html#timers) - for `setTimeout`, `setInterval` mocking.
		- [x] [Mock cheat sheet](https://vitest.dev/guide/mocking.html#cheat-sheet)
- [x] Testing types - relevant for TS
- [x] [Vitest UI](https://vitest.dev/guide/ui.html) - interactive test report tool
- [ ] [Browser mode experimental but recommended](https://vitest.dev/guide/browser/) - headed. minor relevance in volopay. uses webdriverio and playwright. Recommended to avoid flaky tests, confidence against the [simulation caveat](https://vitest.dev/guide/browser/).
- [x] [In-source testing.](https://vitest.dev/guide/in-source.html)
- [x] Test context - control test flow from inside the test. idea is that you're provided latest meta-data and non-void functions in the test codes.
- [x] [Test environment](https://vitest.dev/guide/environment.html) - happy-dom is faster but lacks some APIs compared to jsdom.
- [x] [IDE](https://vitest.dev/guide/ide.html) support - vscode extension
- [x] [Debugging](https://vitest.dev/guide/debugging.html)
- [x] Common errors
	- [x] Relative aliases to be refactored to proper aliases (`URL` [constructor](https://vitest.dev/guide/common-errors.html#cannot-find-module-relative-path))
	- [x] Failed to terminate worker with `fetch` - [link](https://vitest.dev/guide/common-errors.html#failed-to-terminate-worker), config change will fix.
	- [x] Segfaults and native code errors - [link](https://vitest.dev/guide/common-errors.html#segfaults-and-native-code-errors), config change will fix.
- [ ] Improving performance - options, Pool, sharding multiple machines.