# 242. Adding state slices
Created Saturday 30 July 2022

To work with React Toolkit, a React project needs two packages:
1. `@reduxjs/toolkit` - contains core `redux` and extra functionality
2. `react-redux` - React bindings for providing and consuming store state.
   
Note: remove npm package `redux` from `package.json` if present, because it's already present in using `@reduxjs/toolkit`. `import` from `redux` to create store is still valid, although there may be no Intellisense now. It is generally not used when using RTK.

### Working with RTK
There are 5 constructs when working with RTK:
1. Slices - these are combined by RTK to create the whole store. Their function is to separate out reducers and parts of store relevant to a feature. 
   
   The `createSlice` function takes an object with attributes `name` which is a string, `initialState` which is an object, and a `reducers`(**plural**) which is an object of reducer functions.
   A slice is created like so:
	```jsx
	import { createSlice } from '@reduxjs/toolkit';

	const authInitialState = { isAuthenticated: false };

	const authSlice = createSlice({
		name: 'auth', // can be named anything, isn't used elsewhere
		initialState: authInitialState,
		reducers: {
			login: (state) => (state.isAuthenticated = true),
			logout: (state) => (state.isAuthenticated = false),
			checkPassword: (state, action) => (state.existingPassword === action.payload.password)
		}
	})
	```
	
	A slice combines all specified reducers into a *single* reducer accessible via the `reducer` (**singular**) attribute. This reducer is usually exported from the slice file (yes, slices are kept in individual files).
	```jsx
	export default authSlice.reducer;
	```
2. Creating the store - the store is created by combining all the reducers (available in the slices), using the `configureStore` function available in RTK. Note: the `configureStore` param is an object with the attribute of `reducer` (**singular**).
	```jsx
	import { configureStore } from '@reduxjs/toolkit';
	
	const authSlice = /**/ ;
	const counterSlice = /**/ ;

	const store = configureStore({
		reducer: { counter: counterSlice.reducer, auth: authSlice.reducer }
	});

	export default store;
	```
	The `configureStore.reducer` object's keys **don't** have to match the slice name, but they are generally kept the same. But the key is important and used elsewhere.
	
	If there's just a single store, the `configureStore.reducer` can be set to the reducer directly. Like so:
	```jsx
	const store = configureStore({ reducer: counterSlice.reducer }); // also OK
	```
3. Actions - unlike core `redux`, actions strings are not specified by us. RTK action objects which contain unique `action.type` strings. The set of actions available to a slice can be accessed from the slice. These are kept in the slice file, and generally exported where a dispatch needs to be done. Example:
	```jsx
	export const authActions = authSlice.actions;
	```
1. Providing the store - same as before, i.e. by wrapping the React ancestor with `react-redux`'s `<Provider store={}></Provider>`.
2. Consuming the store data - mostly the same as without RTK, i.e. using the `useSelector` hook. The difference is that the data relevant to a slice is actually kept in that slice, and needs to be accessed by the name of slice (specified during slice creation). Example:
	```jsx
	// suppose the relevant slices names' are 'counter' and 'auth'
	import { useSelector } from 'react-redux';
	function MyComponent() {
		const count = useSelector(state => state.counter.count); // instead of state.count
		const authenticated = useSelector(state => state.auth.isAuthenticated);

		return /**/;
	}
	```
6. Dispatch - dispatch are still done using `useDispatch`. The only difference is the way we specify actions. Actions are first accessed from the slice using the `actions` attribute. Then we call a particular action function as per it's name specified in the reducer object of the slice. Note: the action function should be called to generate the action.
   
   We can pass action data to by passing the data directly in the action function. This will be made available an attribute named `payload` in the action object received by the reducer.
   
   Code example:
	```jsx
	import { useDispatch } from 'react-redux';
	import { authActions } from '../auth';

	function MyComponent() {
		const dispatch = useDispatch();
		
		const loginHandler = () => dispatch(authActions.login());
		const passwordHandler = (event) => dispatch(authActions.passwordCheck(event.target.value));

		return /**/;
	}
	```

Note:
1. Name of the slice and name of the slice reducer in `configureStore.reducer` key don't have to match. See [code](https://github.com/exemplar-codes/react-redux-demo/commit/8a09aa87c7c538848d12bcc0774e9c064b6db451).
2. When accessing store data using `useSelector`, the key of the callback param must match the slice reducer name. If there's only one reducer passed directly to `configureStore`, the data is directly accessible. See [code](https://github.com/exemplar-codes/react-redux-demo/commit/d5ca4e7de8525e6a536506f6ff5f29e61acefc2e#diff-5541be143e3e2a0dcdfefeb9ca7c2ac4cb3eb7965e000bd10669f31f125755cf).
3. All data passed to the action creator during dispatch is made available as `payload` in attribute of the action in the slice reducer.
4. Every attribute `reducer` is singular at all places except during slice creation, where it's plural.
5. Store drilling w.r.t slice reducer name is there only when consuming store data, not in the slice's `reducers`.
6. Slices are kept in different files, and only the slice's action creators object and reducer are exported, since they're needed during dispatch and store creation, respectively.

- See [code](https://github.com/exemplar-codes/react-redux-demo/commit/1546db08861125733265e11773d1909acf3fc30c) for this whole page.
- RTK with class based components is also [easy](./237_Redux_with_React_for_class_components.md), because all needed functions `connect`, *mapStateToProps* and *mapDispatchToProps* are all still part of `react-redux` package. See [code](https://github.com/exemplar-codes/react-redux-demo/commit/7c8c403f547abeaf542ff73cb052e1dd46db04a2).


### Questions
1. Can a reducer in a slice access values from another slice? No, each reducer can access only slice in it's data. If two slices wish to use each other's data, they should be combined into a single slice OR one can do some acrobatics to get reducers to share data.
2. Can two slices have data with the same name? Yes, there's no scope of collision as reducers are confined to their own slices. This may cause confusion amongst developers of the project, though. See [code](https://github.com/exemplar-codes/react-redux-demo/commit/8d2ef9f3838979384acec94cb51cf64bfcaff0ca).


FIXME: 
- mention that `createStore`, `createSlice`, `reducer` (with getState), `createAsyncThunk`, `createSelector` are the important things. Everything else is an add on.
- RTK is good enough to be used. Redux (vanilla) can be ignored.
- Side-effects though discouraged, can still be called form async thunks.
- Mentions the few [issues](https://github.com/sanjar-notes/react/issues/33) with RTK