# 1. Auth Flow
Created Sat Dec 30, 2023 at 1:55 PM

## Authentication providers
- There are paid solutions (APIs) one can use for authentication:
	- Amplify by Amazon
	- Firebase by Google
	- Auth0
	But here, we'll focus on building our own backend for auth, instead of using a paid service.

## Authentication flow
Client sends POST to /auth with email and password. Backend returns an auth token if *login* is success, else returns 401 (Unauthorized). If the endpoint is for *signup*, the backend checks if the pair exists, if not, it stores the email and password as a new entry and then returns the auth token. Cool.
   ![](/assets/1-Auth-Flow-image-1-958a31ee.png)

## UI structure for authentication (frontend code)
Essentially have to do something (or exactly) like this.

Make a root level component, then 2 children (called public and private). These children are usually navigation stacks since they contain screens. The root level component has a "user" state which is null initially. The public nav stack has a login screen, a logout success screen, forgot password screen, and possibly more screens like terms and conditions and other non-sensitive stuff.

Private navigation stack can be entered only if `user` object is not null. Consequently the public stack is the default stack. `user` being null signifies user has not logged in. 

The default screen (across app) is the public stack with screen being the login screen. The private stack's default screen is the "Home" screen.

Flow wise, when the app starts, we check to see if we have a saved token in storage (persistent storage), if we do, we make an API call to get latest user info (since user info could have changed from some other device in the worst case, incidentally this API usually called `validate_token`), and set the `user` state if the token is successfully verified by the backend. Since `user` is not null, we navigate to the private stack, with the Home screen showing up. _One optimization is that the validate_token returns the `user`, so we don't have to make another user call to get latest user info_.

Alternatively, if the app start and there is no saved token, we show the login screen. If user logs in successfully, we store the token, make the user API call, set `user` and navigate to the private nav stack (like on previous paragraph), with the Home screen showing up. On log out, we remove token from storage and set user to `null`, automatically navigating us to the public stack, and back at the login screen. 

We can show a "toast" to say logout successful and login successful, this is a good way to avoid screen complexity to show these small messages and also avoid navigation complexities. Btw, the toast is shown when the login or logout API call succeeds, i.e. toast code is a (static) function call. An alternative to showing toasts, is to store the toast in the root state, and render the messages in the `Login` and `Home` screens at a chosen location on the screens. This "on screen" approach also has one advantage, that the message stays persistently on the screen, until the user interacts and tries to do an action. Both are valid approaches, but toast way is simpler.