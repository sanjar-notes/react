# 5. Importing and exporting in React
Created Tuesday 25 August 2020

## Why
As React is made of reusable components, it's obvious that code will need to be imported to other files. Consequently, it must be exported properly.

It is important to note that imports/exports are not specific to React but to version of JavaScript being used. This import and export feature is actually supported by Babel.

## How
### Importing
```JSX
import App from 'components/App' // .jsx or .js can be omitted

function MainApp() {
	return <App />;
}
```
### Exporting
There are 2 ways (syntactic) to export:
```JSX
function App() {	
	return (<div><\div>);
}

export default App; // extra line
```
OR all in one go
```JSX
export default function App() {	
	return (<div><\div>);
} // modular, no extra line
```

### `export` vs `export default`
* `export default`  is useful if only one thing is being imported. Also the imported thing may be renamed at the destination(using **import x from y**). 
* `export` alone exports objects which need to imported by their original name, and separated by commas.
Note: There is atmost one `export default`.

## Example code
Source:
```JSX
export default function App1() {	
	return (<div>App1<\div>);
}

export function App2() {
	return (<div>App2<\div>);
}

export function App3() {
	return (<div>App3<\div>);
}
```

Destination:
```JSX
import AppOne from "./source.js"; // export default - no brace, original name needed

import {App2, App3} from "./source.js"; // export - must use braces and original same

import AppOne, {App2, App3} from "./source.js"; // all in one line
```