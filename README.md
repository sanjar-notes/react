# React.js

[Live link](https://sanjar-notes.github.io/react/home/4_resource_itineraries/2_React_the_complete_guide/12_Behind_the_scenes_of_React_and_optimization_techniques/152_How_React_Really_Works)

## Why
My needs:
1. Break down UIs into small functions
2. Make my own "HTML components"
3. Don't get bogged down writing glue code
4. Use the latest JS syntax without problems

React provides:
1. A sane way to build apps - specify the frames, without worrying about the transition code.
2. Componentization - break down the UI into small reusable (and manageable) parts
3. Simple [DSL](https://en.wikipedia.org/wiki/Domain-specific_language) - it's like HTML except `{js_expression_here}` is used for including JS logic.
4. Modules - JS, CSS files can be imported seamlessly
5. Simple and stable app constructs
6. Community support + [docs](https://react.dev/) + dev tools (the popularity!)

## How
- React uses a [heuristics-based algorithm](https://legacy.reactjs.org/docs/reconciliation.html) to "figure out" transitions between frames automatically.
- It provides simple and stable app constructs (functions that you can import and use), so app development is practically declarative.

## What

React is a declarative way to build user interfaces.
> [React](https://reactjs.org/) is a *library* to *create* and *reuse* your own HTML tags.
> 
> &mdash; Me when I started using React

## Usage
- Browse these notes here on GitHub or just clone the repo, it's [markdown](https://www.markdowntutorial.com/) 🙌. Or see the [website(experimental)](https://sanjar-notes.github.io/reactjs-notes/docs/home/resource_itineraries/React_the_complete_guide/Behind_the_scenes_of_React_and_optimization_techniques/How_React_Really_Works)
- Pre-requisites: basic HTML, CSS, JS. And some [JS syntax sugars](https://kentcdodds.com/blog/javascript-to-know-for-react)
---

These are notes (mental models) I made while doing [this Udemy course(released 2020)](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/).

I have tried to compress and classify information into manageable chunks.
