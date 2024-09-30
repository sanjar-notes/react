# 27. Priority Order for Queries
Created Mon Sep 30, 2024 at 11:51 AM

We looked at 8 types of queries, and some have overlap. So what to prefer.

1. getByRole - preferred for everything.
2. getByLabelText - for form fields
3. getByPlaceholderText - an alternate for field labels.
4. getByText - useful outside of forms. (non interactive elements, messages)
5. getByDisplayValue - for form.input values
<br />

6. getByAltText - not consistent for all browsers.
7. getByTitle - not consistent for all browsers
<br />

8. getByTestId - last resort. Only when text cant be seen or heard. Ex - when the text is too dynamic.
   

## Code implication
This priority also helps in writing the code with least effort. You dont need `data-testid` too much.