# 200. Dealing with form submission and user input
Created Monday 25 July 2022

[Code repo](https://github.com/exemplar-codes/reactjs-forms-user-input)

There are two ways to access user input - `ref` and `onChange`(with state). I already know this. See [onChange](https://github.com/exemplar-codes/reactjs-forms-user-input/commit/a0925ba34d508f3c3f7df1f9f3b8f7175f9e4845) and [ref](https://github.com/exemplar-codes/reactjs-forms-user-input/commit/7ba6b0a577b9009f555457a8d4e24771be89c16b).

Which one to use?
- If input value is wanted only once, i.e. on submission, a `ref` is better.
- If input value is wanted on each keystroke, `onChange` is better.

Note that in both ways, resetting the input is possible, but writing to the DOM (using `ref`) is not a clean way to use React. In short, prefer state if there is need for 2-way-binding (i.e. for input resets), either with `ref` or `onChange`, by setting the `value` property in the `input` tag.

- Remember to clear the input on form submission. Doing this is possible with 2-way-binding, as shown earlier in the course.