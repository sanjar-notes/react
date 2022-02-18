# 1. Conditional rendering in JSX
Created Thursday 27 August 2020

#### Why
This is one of the uses of JSX's treatment of logic-expressions and UI code as inherently coupled.

#### How
Simply use 3 things:
1. Fact that JSX code is an object.
2. AND and OR logical operators evaluate to one of the argument object.
3. `null` renders to nothing in React. 

#### What
These are some cases of conditional rendering using JSX
1. Ternary operator.
```JSX
function App() {
	const name = 'Rahul';
	const isLoggedIn = false;

	return <p> Hello {isLoggedin ? name : 'World'} </p>
}
```
2. AND (&&). Shortcircuiting helps.
```JSX
{!isLoggedIn && <p> Hello World </p>}
{isLoggedIn && <p> Hello {name} </p>}
```
This works because JS **returns** the *second* value as it is(if it is truthy, instead of a boolean), in case of logical AND.
```JS
true && 'Sanjar' // 'Sanjar'
false && 'Sanjar' // false, short circuit
'Sanjar' && 'Afaq' // Afaq
```
For a || (OR), the *first* value is **returned** if truthy, else the *second* value.
```JS
false || 'Sanjar' // 'Sanjar'
true || 'Sanjar' // true, short circuit
'Sanjar' || 'Afaq' // 'Sanjar', short circuit
```
* These statement return a value. So in order to avoid return for the function, we wrap these statements in a {}
3. Using if statements and JSX expressions. This is considered bad practice. This is because it defeats the reason why JSX is created (to include expression code and UI code). It can be done but should never be done.
4. Using switch case.
5. Using {} and JSX inside it. Expression will be returned. JSX is JS too 😂️.

```JSX
return (<div>
			{ false && <p1> Hello <p1>} 
		</div>);
```

- Practical Example: In the robofriends App, we can show loading if the URL is still loading.
```JSX
if (!this.state.robots.length) return <h1>Loading</h1>; // conditional rendering

return (
  <div>
	...// some code
  </div>);
```
* Generally, the conditions are kept inside the return clause, using {} JS if possible.



