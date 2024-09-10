# 7. Using query methods
###### render and screen
- `render` is a function that takes in the component to be rendered.
- `screen` is the object which contains resulting DOM.

Example:
```jsx
import React from 'react';

import { render, screen } from '@testing-library/react';

import App from './App';

it('check if heading is there', () => {
	render(<App />);
	
	const heading = screen.getByText('todo');

	expect(heading).toBeInTheDocument();
});
```

###### Tips
- Basiscally, just use the query method (prefix) with a proper locator (postfix).
- To assert opposite, use `expect.not.`, i.e. just chain `not`.
