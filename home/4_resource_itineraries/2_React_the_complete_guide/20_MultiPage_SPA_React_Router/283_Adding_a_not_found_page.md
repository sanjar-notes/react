# 284. Adding a not found page
Created Sunday 25 September 2022

Add a `Route` with path as `*` (wildcard) as last child of a `Switch`. This makes sure that it renders only if no other route does.