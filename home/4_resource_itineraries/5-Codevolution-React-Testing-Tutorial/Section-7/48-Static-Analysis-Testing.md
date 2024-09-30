# 48. Static Analysis Testing
Created Mon Sep 30, 2024 at 10:26 PM

This is a type of tests where code is not run. It is based on sophisticated pattern matching (but still determinate).

What does static analysis address:
1. Type checks (TypeScript) - catch errors quickly during development time, instead of runtime.
2. Linting (ESlint) - catch bad syntax, and some instances of bad practices.
3. Formatting (Prettier)
4. Commit guards (Husky and lint-staged) - runs the linter on `git commit.`

## Content
- Eslint - vite already has eslint added. However, one can add a lot of good constraints that reduce the chances of bad code.
- Prettier is an opinionated formatting tool. It needs to be installed as an npm package.
	- For auto-formatting code in the IDE, install the vscode Prettier extension.
- [Husky](https://youtu.be/smR351T-roc?si=gcQzsYIWcg1cVcYX) - a guard program that runs (and prevent op) when git `commit` or `push` is attempted with a bad code state. It does this for all files.
- [lint-staged](https://youtu.be/36VhpIIlerQ?si=bH_U_QhVzWRICeXR) - guides Husky to only work on staged files, instead of all files.