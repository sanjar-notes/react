# 205. Refactoring and derived states
Created Monday 25 July 2022

*Nothing new here*.

- The current code is messy and arbitrary, there's no clear structure to it.
- The code is not scalable for additional input values.

- Note that we need just need two states per input - `isTouched` and the `enteredValue` state. Additionally, we need a validation function which works works on the `enteredValue` to determine validity and a conditionally rendered UI to display validation error. So 4 pieces of code per input.

##### Derived states
- Try to use as little states as possible, i.e. use normal variables for states that can be computed using other states. In short, don't use state for derived values of validations.


##### Refactoring
- Try to minimize code repetition.
- Use custom hooks to manage similar types of inputs.