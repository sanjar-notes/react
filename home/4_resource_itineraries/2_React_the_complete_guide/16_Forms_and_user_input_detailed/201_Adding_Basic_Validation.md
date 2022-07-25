# 201. Adding basic validation
Created Monday 25 July 2022

- Client-side validation is good. But client-side validation alone (i.e. without server side validation) is very dangerous. Reason: client side code is accessible to the user, and may be bypassed. In short, server-side validation is a must, irrespective of whether client-side validation exists or not.
- Client-side validation is for UX, not security.
  
[Here](https://github.com/exemplar-codes/reactjs-forms-user-input/commit/0fb8fd49ac8dc6634e35cfdc0217079886477633), I've implemented a basic validation to ignore empty inputs. There's one UX problem though: there's no indication to the user that the input was invalid.