# 3. How React works
Created Tuesday 08 September 2020

### What makes React revolutionary?
In the context of web browsers, changing from a UI frame **E** (for existing) to a UI frame **R** (for required), i.e. E --> R can be done in many ways:
1. Remove **E** elements from the page, then calculate and paint **R**. This is the most expensive thing, computationally. It's very easy to code.
2. Specify what changes need to be done to **E**, to make it look like **R**. The changes keep in mind similar branches of the DOM, so it's economical. This is very cumbersome to code.

Assume all DOM operations, layout calculations and painting to the screen were very cheap to do. One would choose to do it by the first way, i.e. just replacing the page with the new UI. React makes this possible. Of course, it's not magical. There's something called the virtual DOM and diffing algorithm. 

React will change the DOM in the most optimum way, *practically* possible.

[Reflow and repaint, what are they?](https://medium.com/swlh/what-the-heck-is-repaint-and-reflow-in-the-browser-b2d0fb980c08)

### React internals - Virtual DOM and the diffing algorithm
To go from E --> R, React keeps two DOM trees in memory. These in memory DOM trees are called 'virtual DOM'. They are fast to work with, because they are not connected to the webpage. Let's call them pristine and dirty. 

Pristine is a copy of the current actual DOM, and dirty is initially nothing. 
Steps React uses:
1. When the next frame is specified, it creates the *dirty tree* based on it.
2. The pristine and dirty trees are then compared using a diffing algorithm. This results in DOM ops that need to be done to minimally update the DOM. This is called [reconciliation](https://reactjs.org/docs/reconciliation.html#recursing-on-children).
3. These DOM ops are batched together.
4. The batched DOM ops are applied to the actual DOM.
5. Reflow and repaints are done if needed.
6. The dirty tree becomes the pristine tree. And the process is repeated.
Done!

[Virtual DOM and diffing](https://www.pluralsight.com/guides/virtual-dom-difference-maker-react-js)

### More about the diffing algorithm
The generic algorithm for diffing trees is O(n<sup>3</sup>). But React uses a heuristic O(n) algorithm based on two assumptions:
1. Different components will produce different trees.
2. The developer can hint at which [*child*](https://reactjs.org/docs/reconciliation.html#recursing-on-children) elements may be stable across different renders with a [key](https://reactjs.org/docs/reconciliation.html#keys) prop.

["In practice, these assumptions are valid for almost all practical use cases."](https://reactjs.org/docs/reconciliation.html#motivation)