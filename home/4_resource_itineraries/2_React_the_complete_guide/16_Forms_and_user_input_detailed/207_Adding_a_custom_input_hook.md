# 207. Adding a custom input hook
Created Tuesday 26 July 2022

The current [code](https://github.com/exemplar-codes/reactjs-forms-user-input/commit/4d9a91e8d013df60f031a4ced64e149f082f33e6)still has a repetitive structure, in that each state has a *isValid* and *value* state. We can abstract this out to a custom hook.

Steps to make the custom hook:
1. Copy all code relevant to a state in the hook.
2. Rename stuff to be generic in the hook.
3. Add any arbitrary code to be taken as parameter, e.g. the validation logic in this case.
4. Return whatever is *used* in component.

See [result](https://github.com/exemplar-codes/reactjs-forms-user-input/commit/7c091cddd97723b9ba21ae4d9d35cd3b3d362edd). This code has less repetition and code for the component is focused on UI instead of form logic.

Note: Alternatively, we can make custom Input component that work for multiple kind of inputs.