# 154. A closer look at child component re evaluation
Created Monday 04 July 2022

### Component re-evaluation causes re-running of child components too
On re-render, the function re-executes, which includes re-execution of all UI component it returns. Example:
```jsx
	function MyComponent() {
		// some state logic
		return <><A /> <B /> <C /></>;
	}
```
On re-render, the function 'MyComponent' will re-run, and so will the functions for component 'A', 'B' and 'C'. Note that this will continue recursively for all components used by A, B, C too. Also it does not matter if their props change or not, i.e. React *will* re-run the component functions even if props haven't change. Yes, this is inefficient.
	
Of course, only differences will be updated in the real DOM, i.e. re-evaluating component function does not necessarily lead to a re-render of the DOM. Reason: React DOM diffing.

---
- Child component re-renders don't re-initialize their state. i.e. a child component preserves state between re-renders.