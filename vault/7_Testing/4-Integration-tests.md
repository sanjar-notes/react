# 4. Integration tests
Created Tue Sep 17, 2024 at 11:35 AM

TLDR; choosing Playwright, due to better DX (debugging) and IDE support.
## Cypress
- Intro - https://youtu.be/BQqzfHQkREo?si=CnOPLuI5EkPYPehP
- Docs - https://docs.cypress.io/guides/overview/why-cypress/
- [Notion - Testing volopay priorities](https://www.notion.so/sanjarcode/Testing-volopay-10420b93200480619b2fed5a9ed90d51?pvs=4)

### Features
- Has [fluent](https://mtlynch.io/notes/cypress-vs-playwright/#cypress-syntax-is-more-consistently-fluent) interface. Pro.
- No file uploads by default. Con
## Playwright
- Playwright is better is the prevailing opinion. 
	- https://mtlynch.io/notes/cypress-vs-playwright/#my-prior-experience-with-cypress-and-playwright
	- https://www.reddit.com/r/QualityAssurance/comments/1437c5d/deciding_between_playwright_vs_cypress/
	- Codegen is possible using VScode IDE. 
		- Pause watch also triggered from here.
		- Test reports, reruns can be accessed.
	- Runs UI in the browser, and not its own app.
	- Pause, inspect in Browser DevTools is possible
	- Logging works as usual using `console.log`
	- Has lesser open bugs.
	- Faster (than Cypress) - runs tests in parallel. A [tad faster](https://www.checklyhq.com/blog/puppeteer-vs-selenium-vs-playwright-speed-comparison/) than Puppeteer.
	- Less stable than Puppeteer.
	- [Debugging is simpler](https://playwright.dev/docs/debug#vs-code-debugger) - can be done in vscode, and realtime UI stepping is supported. Live debugging can also be done.
	- Can record videos. Useful for failed tests.

- Even in headless mode it still runs a real browser, just with no UI. So headed vs headless is not much difference, perf wise, except the DX (no distractions) and that PW can run in CICD.
### Features
- [Auto wait feature.](https://playwright.dev/docs/writing-tests#:~:text=playwright%20automatically%20waits%20for%20the%20wide%20range)
- Has [imperative interface](https://mtlynch.io/notes/cypress-vs-playwright/#cypress-syntax-is-more-consistently-fluent), just like RTL. Con, but better than Cypress if you're using RTL. Keeps the language the same.
- File uploads
- CICD - `npm run`, compared to Cypress Docker.
- Supports multiple browsers - Chrome, Firefox.
- Supports multiple languages - JS, TS, Python, Java, C#

## Puppeteer
Playwright > Puppeteer as per online opinion.
But both have almost the same functionality.
### Features
- Codegen
- Has more plugins than PW. Pro.
- Supports only JS.
- More community support. Preferred for beginner level (test) teams, and fast deadlines.
- Con: Puppeteer does not offer a way to handle file downloads in a programmatic way