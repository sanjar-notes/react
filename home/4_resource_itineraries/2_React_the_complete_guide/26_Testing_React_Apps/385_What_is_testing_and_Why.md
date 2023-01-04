# 385. What is testing and Why?
Created Wednesday 4 January 2023

- We *have* done testing in this course, but it manual testing.
- Manual testing is not scalable, at all. It's also error prone.

## Why
The sole goal of automated testing to detect regressions. That's it.

A regression is said to have occurred if the code breaks when some changes are made to it, and it was working fine previously. Example - we made a change to a core UI component that is not backwards compatible, which broke some feature which used this component.

In a medium to large sized app, it's not practical to manually check every feature/page/flow/combination for every change we make to our code.

By detecting regressions (by writing automated tests), we:
1. **Save time and effort** - We can fix issues as soon as they show up. This saves us a lot of time, as compared to detecting an issue later where we may need to debug/re-write code at all places that used this buggy part.
2. **Gives us confidence** - we have confidence that, atleast, minor bugs are not present in our codebase.
3. **Makes experimenting easy** - we can try out changes to our code without worrying about unknown regressions, because we can detect them.
4. **Generate data about code quality/architecture** - we generate useful data that might be kept in mind when making future changes.
5. **Learn how to write good code** - consequence of \#4.
   
![](../../../../assets/Pasted%20image%2020230104193538.png)


## How
- An automated test is just code that checks our app code. Yeah, kind of meta, but very useful.
- We poke the system mimicking possible user events, and make sure the effects are how they should be.
- We can test small isolated parts, as well as whole flows.


## What (details)
"Automated testing" is a very broad definition in software development. The way it is done varies w.r.t the domain, criticality of app etc.

Examples:
1. Frontend web apps - we need a sample browser, where we automatically load, mimick events and see the result by inspecting the DOM.
2. Backend web apps - we need a server running in test mode, where we mimick incoming requests and database reads/writes and verify if everything went OK.
   
We need 4 tools to do automated testing:
1. Environment simulator - headless browser, inspected VM. We simulate the whole lifecycle of the app here, including setup, mimicking events, results etc.
2. Environment inspector - DOM APIs, OS level inspector. We inspect changes, results for events that we mimick.
3. Assertion tool - compare resultant environment values with ideal values, to see if they match, strictly or loosely. This is kind of a library/syntax-sugar thing, so we don't have to write stuff from scratch.
4. Test runner - a tool that runs various tests and creates/prints reports of what failed/succeeded. This tool also understands/specifies how tests are written - e.g. files, suites, clauses and single tests.