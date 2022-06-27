# 129. Forward refs
Created Tuesday 06 May 2022
- [ ] in vault

### Why
- The `useRef` hooks works on HTML elements only, and not custom components.
The forward ref functionality let's one add refs to custom components too, so that they can be controlled directly (without the need of state/re-renders).
- It's rarely used.

### How
Here's an example. We use ref on a custom component, just like a ref is added to an HTML element.
```jsx
import {useRef} from 'react';

function MainApp() {
	const inputRef = useRef();
	
	/* some logic using inputRef.current */
	
	return <Section ref={inputRef} />;
}

export default 
```

We need to drill down the component chain using `forwardRef` for each component in the chain, and add `ref`,  till we reach an HTML element, where we also add a `ref`. The `ref` on the top of the chain will now reference the HTML element at the bottom of the chain.
```jsx
const Section = React.forwardRef((props, ref) => <input type='text' ref={ref} />);

export default Section;
```