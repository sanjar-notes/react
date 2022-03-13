# 107. Controlled and uncontrolled components
Created Saturday 5 March 2022
- [ ] in vault

**Note, this is about jargon.**

#### Where is this applicable
In forms, mostly.

#### What does controlled mean
- Controlled components are React components where the state is controlled using React `useState` or a similar thing.
- Uncontrolled components on the other hand, are components where the state controlled by the traditional DOM, not React code variables.

##### Example
- Uncontrolled: When using `input` HTML elements with `useRef`, it would be uncontrolled component as the `input` value is stored in the DOM as default `HTML` behavior, and not a part of state.
- Controlled: This is a different implementation of the uncontrolled case. Here, if the`input` `value` was set to a state variable from `useState` and was actively being set/read from the `input` on `onChange`, this would be a "controlled" component.

#### Differences between uncontrolled and controlled components
- Controlled components are predictable because all state is there in the React (app) code instead of the DOM.
- Uncontrolled components are not no predictable, because the state is actually stored in the DOM and has the life-cycle and properties of the DOM.
- Controlled components actively track input in `form`s and can be used for active validation (i.e. without submission), this not possible with uncontrolled components.

In short, if `form` values are using a state from `useState` (or similar) it is controlled, otherwise uncontrolled.

#### Good Practice
React developers recommend using controlled components for form elements. But it is not a hard and fast rule.


For more info, see: https://reactjs.org/docs/uncontrolled-components.html