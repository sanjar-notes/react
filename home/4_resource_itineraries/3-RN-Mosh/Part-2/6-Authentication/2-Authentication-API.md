# 2. Authentication API
Created Sun Mar 10, 2024 at 12:05 PM

This is the API (or set of APIs) used to login and validate stored tokens.
1. Login - client sends email, password combo. It it's valid, the API returns a token, which is stored persistently by the client. This token is sent as `Authorization` header of all subsequent requests.
2. validate_token - when the client re-opens the app, the first API call is to validate the token and also get latest user info. If the token is valid, the app keeps working as usual, if it's invalid, the client deletes the stored token and the user has to login again.

For all protected APIs, a common pre task is to check the `Authorization` header for each request. 