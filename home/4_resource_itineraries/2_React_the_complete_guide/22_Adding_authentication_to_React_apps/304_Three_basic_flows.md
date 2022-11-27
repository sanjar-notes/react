# 304. Three basic flows
Created Sunday 20 November 2022

## Code - sign up, sign in, access protected content/server-action
1. Create a global state (I'm using Context API), to store the token and "loggedIn" derived state. Also include a `setToken` function.
2. Three actions are possible now:
	1. Sign up - get the credentials from a form, send the email and password, and if there are no errors, store the received auth token(called `idToken` in Firebase Auth). This token will need to be included in all subsequent requests after login (sign up may be considered login, assuming there's no bot verification, for simplicity).
	2. Login - get the creds, send them. There's no need to use the token, since credentials are enough. But do update the stored token, as it may have expired.
	3. Access protected resource - include the token in all requests for protected content/server-actions. The server may be instructed to return the token in every response, so token expiry doesn't trigger a need to re-login.

The location of token in the request is decided by the backend creator. Most common locations are:
1. In the `request.body` 
2. In `request.headers.Authorization` (value will be `Bearer {token}`).
3. As a query string, e.g. `[link]?token=[token]`.

In any case, using HTTPS is very important for all auth traffic, atleast.

Code: from [here](https://github.com/exemplar-codes/react-auth-basic-practice/commit/96512287b1f38a41e8c3d0ab808d070fcc45ce60) to [here](https://github.com/exemplar-codes/react-auth-basic-practice/commit/9b0b3398668295488292e0494df6f18b38b95ff3).