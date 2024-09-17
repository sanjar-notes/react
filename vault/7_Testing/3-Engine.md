# 3. Happy DOM
Created Fri Sep 13, 2024 at 10:08 AM

## DOM envs
This is a simulated browser used for testing.

## `happy-dom` vs `jsdom`
- 7x [faster](https://github.com/capricorn86/happy-dom/wiki/#performance) than JSDOM
- jsdom is more stable. happy-dom has bugs.
- 
## jsdom features
- waitUntilComplete is not present.
- Vitest and RTL support it.
### Happy-dom features
- Supports Vitest and RTL by default, [see](https://vitest.dev/config/#environment). Small [caveat](<https://github.com/capricorn86/happy-dom/wiki/Setup-as-Test-Environment#vitest:~:text=Link%20to%20guide-,timer%20functionality,-happyDOM.waitUntilComplete()%20and>).
- Browser APIs
- File reader
- Form data
- Cookies
- Clipboard
- Iframes
- Form validity state
- Web components

- waitUntilComplete - waits for all operations on the page to complete (fetch, timers etc)
- waitForNavigation
### jsdom
- Supported by Vitest and RTL by default.
- Cookies
- [List of CSS selectors](https://github.com/dperini/nwsapi/wiki/CSS-supported-selectors)

- No loaded check detection. Requires contextual workaround.`

## Docs
- [Getting Started](https://github.com/capricorn86/happy-dom/wiki/Getting-started)
- [Use as Test Environment](https://github.com/capricorn86/happy-dom/wiki/Setup-as-Test-Environment)
- Mocking (use Vitest.vi, jest.spyOn) - [Vitest](https://github.com/capricorn86/happy-dom/wiki/Setup-as-Test-Environment#vitest-1)

## Problems
- jsdom is comprehensive and stable.
- happy-dom has many unresolved issues with basic functionality


## Drop-in replacement
The test code depends on the runner/framework and the UI lib, and not on the rendering engine, so its quite possible to switch the engine anytime.

However, to ensure you can easily switch between DOM engines like JSDOM and Happy DOM, it's important to avoid relying on engine-specific features or quirks. Here are a few guidelines:

1. **Stick to Standard DOM APIs**: Use APIs that are part of the standard DOM specification, which are likely to be supported consistently across different engines. Avoid using engine-specific methods or behaviors that aren’t standardized.

2. **Test Browser-like Behavior, Not Engine Implementation**: Write tests that focus on how a user would interact with the application (e.g., clicks, form submissions) rather than testing the internal mechanics of the DOM engine. This helps ensure that your tests remain engine-agnostic.

3. **Avoid Engine-Specific Workarounds**: Some DOM engines may have bugs or incomplete features, which might tempt you to write engine-specific workarounds. Instead, if you encounter issues, consider filing a bug or finding an alternative approach that works across engines.

4. **Abstraction Layer**: If necessary, you can introduce an abstraction in your test setup, where you can switch between engines easily (e.g., with a configuration flag). This allows you to test across multiple engines if needed, ensuring consistency.

5. **Run Tests on Multiple Engines**: If compatibility is a concern, run your tests on both JSDOM and Happy DOM as part of your CI pipeline to catch any discrepancies early on.

By adhering to these principles, you'll ensure that your tests remain flexible and portable across different DOM engines.

## Conclusion