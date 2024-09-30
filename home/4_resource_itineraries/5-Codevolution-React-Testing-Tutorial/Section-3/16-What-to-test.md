# 16. What to test
Created Fri Sep 27, 2024 at 5:45 PM

There are no rules. But there are some guidelines.

What to test:
1. Component renders without errors
2. Component renders with props - is the HTML correct for different props.
3. Component renders in different states. e.g. if logged in, 'Sign out' should be visible, otherwise 'welcome' should render.
4. Component reacts to events, clicking a button works or not.


What not to test:
-  Dont test implementation details
- Third party code - dont test MUI components because its already tested.
- Code thats not important from a user point of view.