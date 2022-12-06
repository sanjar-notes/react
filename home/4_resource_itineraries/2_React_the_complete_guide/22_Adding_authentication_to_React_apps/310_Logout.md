# 310. Logout
Created Sunday 20 November 2022

## Logout procedure
The server, in case of auth tokens, doesn't care about the login state of the user. This means  that there's no need to send a request when the user logs out.

So, just reset the token to be empty, and we're done.

[See code](https://github.com/exemplar-codes/react-auth-basic-practice/commit/78f744857ce71f75b59346ffcaa587c69afe48b8)