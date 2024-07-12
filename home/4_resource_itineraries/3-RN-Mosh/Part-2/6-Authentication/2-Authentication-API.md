# 2. Authentication API
Created Sun Mar 10, 2024 at 12:05 PM

This is the API (or set of APIs) used to login and validate stored tokens.
1. Login - client sends email, password combo. It it's valid, the API returns a token, which is stored persistently by the client. This token is sent as `Authorization` header of all subsequent requests.
2. validate_token - when the client re-opens the app, the first API call is to validate the token and also get latest user info. If the token is valid, the app keeps working as usual, if it's invalid, the client deletes the stored token and the user has to login again. *Actually, we don't need this, as we'll get a 401 anyway (leading to a logout) or some other failure code (leading to use of the refresh token)*.
3. Logout - clear the tokens and all fetched data.
4. Timeout - we keep track on BE, and when client receives a 401, then the app logs out.
5. Refresh token - needed in case of micro-services architecture, and to keep tokens fresh (resource and auth servers are different, and changing user auth would need a new token, so).

For all protected APIs, a common pre task is to check the `Authorization` header for each request. 