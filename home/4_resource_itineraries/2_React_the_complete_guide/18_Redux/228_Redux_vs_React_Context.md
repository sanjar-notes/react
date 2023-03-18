# 228. Redux vs React Context
Created Wednesday 27 July 2022

- Both React Context and Redux help avoid prop-drilling for cross-component and app-wide state. Why use Redux then?
  
React Context has some *potential* disadvantages, like:
- Complexity:
	1. React Context can lead to complex code, for larger applications.
	2. React Context providers need to nested within one another for UI components, which looks bad. Example:
		```jsx
			return (
				<AuthContextProvider>
					<ThemeContextProvider>
						<UIInteractionContextProvider>
							<MultiStepFormContextProvider>
								<UserRegistration />
							</MultiStepFormContextProvider>
						</UIInteractionContextProvider>
					</ThemeContextProvider>
				</AuthContextProvider>
		);
		```
	   If less contexts are used to avoid this nesting, the provider components get bloated with unrelated data. For example, theme and auth are completely unrelated, but are together in:
		```jsx
		function AllContextProvider() {
		  const [isAuth, setIsAuth] = useState(false);
		  const [isEvaluatingAuth, setIsEvaluatingAuth] = useState(false);
		  const [activeTheme, setActiveTheme] = useState("default");
		  const [ ... ] = useState(...);
		  
		  function loginHandler(email, password) { };
		  function signupHandler(email, password) { ... };
		  function changeThemeHandler(new Theme) { };
		  
		  return <AllContext.Provider></AllContext.Provider>;
		}
	
		```
- Performance - React Context is OK for low frequency updates like theme, auth change. For high frequency updates, use Redux.
	> My personal summary is that new context is ready to be used for *low frequency unlikely updates (like locale/theme)*. It's also good to use it in the same way as old context was used. I.e. for static values and then propagate updates through subscriptions. It's *not ready* to be used as a replacement for all Flux-like state propagation. [Source](https://github.com/facebook/react/issues/14110#issuecomment-448074060)
	
Note: Both React Context and Redux may be used for different parts of an app, or use just one of them.