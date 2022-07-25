# 197. What's so complex about forms?
Created Sunday 24 July 2022

##### Observation
- Forms seem simple and trivial, but they are **not**. They can be even be considered *complex*, from a developer perspective.
	- This is because a form is essentially a set of inputs, i.e. the state of a form to be valid/invalid is a complex one determined by the all the entered inputs.
	- Each input may have it's validations, in addition to secondary validations (i.e. the coherence of entered inputs with each other) or "dynamic" validations, i.e. one may need to run validations w.r.t existing data of the app, thus requiring communication with the server.
	- Each input may also have multiple error messages that should be displayed, depending on the entered input and it's relation to other dependent inputs.
	![](../../../../assets/Pasted%20image%2020220724171154.png)

##### When to validate
A complex part of forms is the displaying of messages for invalid inputs. The question is - when to validate? There are 3 ways to validate:
1. When the form is *submitted*
	- Pros
		- Blank/initial warning, is avoided, i.e. when the form has just loaded.
		- Easy to code.
	- Cons
		- Feedback is too late, especially for long forms.
		- The user may need to manually go back to the invalid user input.
2. When a input is *losing focus*
	- Pros
		- Blank/initial warning, is avoided, i.e. when the form has just loaded.
		- Feedback is better than on form submission.
	- Cons
		- Error message for input is removed when the user is correcting the invalid input.
3. On every keystroke (or input change)
	- Pros
		- Immediate feedback.
	- Cons
		- There's are blank/initial warnings, when the form loads, which may be annoying.

Of course, we can use a combination of these for different inputs.
![](../../../../assets/Pasted%20image%2020220725102803.png)