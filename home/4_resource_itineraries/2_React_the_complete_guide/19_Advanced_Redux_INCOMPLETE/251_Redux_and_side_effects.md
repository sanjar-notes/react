# 251. Redux and side-effects
Created Friday 19 August 2022

### Situation
An app certainly has asynchronous and side-effect code. Redux, on the other hand, has a core principle regarding _reducers_ - Reducers must be pure, side-effect free and synchronous functions.

FIXME - why should reducers be pure in Redux? Maybe to allow for time travel debugging.

This, of course, does not mean that we cannot work with Redux in code involving non-pure operations. It's just that _reducers_ constrained to be pure. So there are two ways to work with Redux with non-pure code:
1. Run dispatch as needed, inside non-pure code too. Absolutely OK. Code, if used often, is somewhat "all over the place".
2. Create an "action creator", which can be an impure function but returns an action object which can be used for dispatch. This "hack" is called a "thunk action creator" in the Redux community. Redux has provisions for making thunk action creators and provides the function with necessary Redux functions like `dispatch`, `getState`, by using `redux-thunk` middleware package.

### Action Creator architecture
Action creator, in it's simplest form, is something like this:
```js
function MyActionCreator(payload) {
	return { type: 'MY_STRING', payload };
}
```
This is fine for avoiding extra string code, and is used.

But the popular definition of "action-creator" is not that of a function that *merely* "returns an action". So what is it then? Let's see.

An action creator that has side-effects but everything is synchronous, will look like so:
```js
import store from './path';

function MyActionCreator(payload, config) {
	doSomething...;
		
	store.dispatch(...);
	...
	store.dispatch(...);
	...
	store.getState();

	return {type: 'MY_STRING', payload};
}
```
This is fine.

But what about an action creator that must run async operations.
Let's try:
```js
import store from './path';

function MyActionCreator(dispatch, getState, payload) {

	(async function() {
		await doSomething...;
			
		store.dispatch(...);
		...
		store.dispatch(...);
		...
		store.getState();
	})();
	
	return {type: 'MY_STRING', payload};
}
```
Would this work? No. We will return before the computation of the async function ends. Observed carefully, it is impossible in JS to return a value from a function after doing async ops. At best, you can return a promise with a return value.

Now, the action creator was an async function itself (i.e. it returned a promise with the action value), we would need to change the Redux API to something like so:
```js
import store from './path';

myActionCreator().then(action => store.dispatch(action));
```
But this is the same as using store between async functions, which we can do already (the first option). This also makes action creators of two types - synchronous and asynchronous ones. This is resolved by the architecture Thunk architecture Redux uses.

### Thunk architecture in Redux
So what's the architecture of thunks?
- Redux solves the problem of two kinds of action creator (thunks) by mandating that all thunks be *synchronous* (but may run side-effects).
- Instead of returning an action object, thunk creators return a callback function (the thunk) which either returns an action object or a promise that does.
```js
// Creating the thunk
function myThunkCreator(payload) {
	return () => {type: 'MY_STRING', payload};
}

function myAsyncThunkCreator(payload) {
	return async () => { 
			...; 
			...; 
			return {type: 'MY_STRING', payload}
		};
}

import store from '../path';
// using the thunk - Note, we need to call(()) the thunk
store.dispatch(myThunkCreator());
store.dispatch(myAsyncThunkCreator());

// BOTH have same structure - return a function (which can be async)
```
Additionally, Redux provides `dispatch, getState` to thunks, so they may run multiple dispatches. All in all, the thunk syntax is:
```js
function myThunkCreator(thunkArg) {
	return [async] function ({dispatch, getState}) {
			
		}
}
```

FIXME: this is incomplete, and has errors.