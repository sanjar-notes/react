# 153. Component updates in action
Created Monday 04 July 2022

- I know that component functions are re-run on state change, but the DOM only updates diffs, and does not re-render everything. 
	- Coded up an example here, see [code](https://github.com/exemplar-codes/assorted-reactjs-apps/commit/a3efefa66142ad22db73bc9017d578b53504823d) + [live app](https://exemplar-codes.github.io/ComponentUpdatesInAction#).
	- The diffs can be seen by flashing of tags in the Elements tab of DevTools.
- It should be noted that all changes to the UI are caused by state changes, i.e. re-rendering takes place only if there's some state change.