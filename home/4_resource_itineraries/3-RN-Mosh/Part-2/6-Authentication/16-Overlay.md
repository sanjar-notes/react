# 16. Overlay
Created Sat Dec 30, 2023 at 1:56 PM

This is used for important loaders (i.e. on form submit)

Since this covers the whole app, we need it at as an ancestor, not some nested child. The show/hide can be controlled by top level state like Redux/Context.

### Root component
```jsx
const isAppLoading = useSelector(isAppLoading); // Redux for example

const overlayStyles = { // example
	position: "absolute",
	opacity: 0.8,
	zIndex: 1,
	backgroundColor: "#ffffff",
}

return (isAppLoading ? <LottieView styles={overlayStyles} />: <App />);
```

### Specific screen
No change in UI, just see the global state to be true and false (on success or on failure of API, btw)
```jsx
export default function SomeSpecificScreen() {
  ...
  const onSubmit = () => {
	  ...
	  ...
	  dispatch(setIsAppLoading(true));
	  await myAPICall();
	  dispatch(setIsAppLoading(false));
  }
  ...

  return <FormScreenAsUsual />
}
```