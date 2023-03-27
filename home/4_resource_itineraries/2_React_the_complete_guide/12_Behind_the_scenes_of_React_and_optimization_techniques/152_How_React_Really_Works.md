# 152. How React Really Works
Created Monday 04 July 2022

The React library is actually the set of two libraries:
1. `react`  - "A JavaScript library for building user interfaces": Contains logic for diffing, component tree, props, state/context. It is oblivious of the browser and DOM, i.e. it works with an abstract UI tree. `react` hands the UI tree "differences" to `react-dom` in case of web apps.
2. `react-dom` - "interface to the web": Contains logic to mutate the real DOM based on the "differences to be made" - provided by `react`.

![](/assets/152_How_React_Really_Works-image-1.png)

### Re-evaluating component function  !==  Re-rendering the DOM
![](/assets/152_How_React_Really_Works-image-2.png)

Changes are made only if they are required. If the HTML already exists, no change to the real DOM is made.
![](/assets/152_How_React_Really_Works-image-3.png)
