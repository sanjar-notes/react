# 5. Until section 5
Created Wednesday 16 February 2022

I've already incorporated my learnings into the mental model.
There is something though.
- Forms - React forms usually use `event.preventDefault()` for forms, and use two-way binding (for resetting value after submission) and use `onChange` with state for all arguments. This way, we store the blanks even after the form is submitted. This data is sent away using a REST API or something.