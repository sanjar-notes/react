# 1. React lifecycle
Created Tuesday 30 May 2022

### Why
It is important to know and understand the component/app lifecycle in React in order to correctly:
1. Handle and clear event listeners
2. Run code at various phases

### How
These are implemented in the library.

### What
There are four different phases in the lifecycle of React component. They are:
1. **Initialization**: During this phase, React component will prepare by setting up the default props and initial state for the upcoming tough journey.
2. **Mounting**: Mounting refers to putting the elements into the browser DOM. Since React uses VirtualDOM, the entire browser DOM which has been currently rendered would not be refreshed. This phase includes the lifecycle methods `componentWillMount` and `componentDidMount`.
3. **Updating**: In this phase, a component will be updated when there is a change in the state or props of a component. This phase will have lifecycle methods like `componentWillUpdate`, `shouldComponentUpdate`, `render`, and `componentDidUpdate`.
4. **Unmounting**: In this last phase of the component lifecycle, the component will be removed from the DOM or will be unmounted from the browser DOM. This phase will have the lifecycle method named `componentWillUnmount`.

Here're the phases:
![](../../assets/pasted_image002%201%201.png)

Here's an image showing life-cycle methods of the phases:
![](../../assets/Pasted%20image%2020220530020206.png)

FIXME: merge the successive page into this