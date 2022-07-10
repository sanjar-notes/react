# 158. Component instance and state
Created Monday 11 July 2022

![](../../../../assets/Pasted%20image%2020220711033742.png)
- When a stateful component is evaluated, React attaches the state to the component's instance.
- As seen previously, `useState` is only run once, on first evaluation, and ignored on all subsequent re-evaluations.
- The state remains attached every component's instance, irrespective of its or its ancestor's re-renders/re-evaluation, until the component is removed from the DOM. If a component is unmounted from the DOM, the state is freed, and when it's reattached, the state is reset (i.e. initialized with the default value generally specified in `useState`).
	- In other words, all stateful components (their instances to be precise) of the UI tree maintain their own state, until they are unmounted. The state resets only upon mounting of a component.
	- Note that re-mounting is treated the same as unmounting + fresh mount. i.e. state is not remembered by default on remount.
- This component instance-state bridge is provided by React.