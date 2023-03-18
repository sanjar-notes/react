# 311. Protected pages
Created Sunday 20 November 2022

## Situation
When the user is not logged in, they shouldn't be able to access the change password page, which they can do now, by manually changing the URL.

## Solution
We need something like "navigation guards". It's a fancy term where the routes are dynamic based on logged in status. Basically, we render protected pages only if they are logged in.

Generalizing this, one can set different guarding criteria for all parts of the app.

Note, it's good to redirect (or show a message) if the user tries to access a protected page.

## Note
"Navigation guards" are implemented on the client side, and, technically speaking, they can be disabled/changed. But we don't need to worry about this, since the user will still need to send the auth token to access protected content/data.

In any case, one should never rely on client side code for security.

[See code](https://github.com/exemplar-codes/react-auth-basic-practice/commit/04d47ed555dd3d897492f0cfe5fd91d89c292cee)