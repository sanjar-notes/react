# 4. Two way Binding
Created Monday 07 February 2022

## Why
In forms, we usually need to save the state to then do a PUT/PATCH call to the server asynchronously. This is easily done using `useState`. But how do we reset inputs to their default value (or blank).

Binding state to change in input tag is one-way binding. But we can also bind the input attribute `value` to the state. This way, when we clear the state (programmatically), the inputs are also reset (in UI), on submission. This is a **two way binding**. And it's mostly used in forms.

## How
Here's a component that uses two way binding:
```jsx
import React, { useState } from "react";

import "./ExpenseForm.css";

function ExpenseForm() {
  const [enteredTitle, setEnteredTitle] = useState("");
  const [enteredAmount, setEnteredAmount] = useState("");
  const [enteredDate, setEnteredDate] = useState("");

  const titleChangeHandler = (event) => {
    setEnteredTitle(event.target.value);
  };
  const amountChangeHandler = (event) => {
    setEnteredAmount(event.target.value);
  };
  const dateChangeHandler = (event) => {
    setEnteredDate(event.target.value);
  };

  const submitHandler = (event) => {
    // this is called when submit is clicked
    event.preventDefault(); // prevent default submit

    // entered data is saved
    const expenseData = {
      title: enteredTitle,
      amount: enteredAmount,
      date: new Date(enteredDate),
    };

    console.log(expenseData);

    // clearing/restting the input fields
    setEnteredTitle("");
    setEnteredAmount("");
    setEnteredDate("");
  };

  return (
    <form action="POST" onSubmit={submitHandler}>
      <div className="new-expense__controls">
        <div className="new-expense__control">
          <label htmlFor="title">Title</label>
          <input
            type="text"
            name="title"
            value={enteredTitle} // for two way binding
            onChange={titleChangeHandler}
          />
        </div>

        <div className="new-expense__control">
          <label htmlFor="amount">Amount</label>
          <input
            type="number"
            name="amount"
            min="0.01"
            step="0.01"
            value={enteredAmount} // for two way binding
            onChange={amountChangeHandler}
          />
        </div>

        <div className="new-expense__control">
          <label htmlFor="date">Date</label>
          <input
            type="date"
            name="date"
            min="2019-01-01"
            max="2022-12-31"
            value={enteredDate} // for two way binding
            onChange={dateChangeHandler}
          />
        </div>
      </div>
      <div className="new-expense__actions">
        <button type="submit">Add Expense</button>
      </div>
    </form>
  );
}

export default ExpenseForm;
```

As said, it's quite useful in forms.


## What
To add two way binding, create a state and use both the value and state updater function (as onchange) on the UI element.
```jsx
const [name, setName] = useState('');

// setName -> changes value and re-renders -> new UI has new `value` prop. Ok
// User event -> triggers onchange -> changes value and re-renders -> new UI has new `value` prop. Ok
// i.e. 2 way binding achieved

return <input value={name} onChange={(e) => setName(e.target.value)} />;
```