# 5. Redux
Created Tue Jan 9, 2024 at 12:56 AM

## Redux the package
Redux is an *efficient* global state management tools. It works by establishing a "store", which is a collection of data and functions (mostly pure).

It is platform agnostic, but generally used for the frontend, especially with React.

The paradigm in apps using Redux is to subscribe some code to the store, which will will run the code when "observed/interesting" piece of data in the store is changed. This observed data has to be specified before hand of course.


### Redux Toolkit
Redux itself [says](https://redux.js.org/introduction/getting-started) recommends using Redux Toolkit over plain Redux.
And plain Redux was indeed, too cumbersome to write.


## react-redux
This is a library, from the same team as Redux that makes it super easy to subscribe to the store. It exposes two hooks `useDispatch` and `useSelector`, which are used for running an action and getting latest value, respectively.

Of course, `useSelector` is the one that creates and maintains the subscription to the store. Consequently, if the data you're interested in changes, your component(s) will automatically remount. Cool.

## TBD
I already covered Redux in Max's course. And have been using RTK at Volopay for ~1.5 years. I didn't do any courses on Redux in this time, but RTK has been an absolute delight, and I've learnt:
1. How to setup
2. Make API calls with the store involved, aka thunks
3. Handling pagination via RTK
4. onSuccess, onError are impure but OK to be called in a reducer/thunk. Maybe there's a better way, idk
5. Problems with selectors - cannot be parameterized. Although the callback notation works just fine.
6. Multiplicity/instantiation problem - easily solved by creating a reducer that injects new object. And using the callback notation for selectors.

// finish these points, add some code examples and details