# 158. Component instance and state
Created Monday 11 July 2022

![](assets/159_Component_instance_and_state-image-1.png)
- When a stateful component is first evaluated, React attaches it's state to the component's instance.
- As seen previously, `useState` is only run once, on first function evaluation, and ignored on all subsequent re-evaluations.
- The state of a component's instance remains attached to it, irrespective of its or its ancestor's/descendant's re-renders/re-evaluations, until the component is removed from the DOM. When the component is unmounted from the DOM, the state is freed, and when it's reattached, the state is reset (i.e. initialized with the default value generally specified in `useState`).
	- In other words, all stateful components (their instances to be precise) of the UI tree maintain their own state, until they are unmounted.
	- Note that re-mounting is treated the same as unmounting + fresh mount. i.e. state is not remembered by default on remount.
	- Conditional rendering change is the same as re-mounting too. See [live](https://exemplar-codes.github.io/ComponentStateBridge#).
- This component instance-state bridge is provided by React.
