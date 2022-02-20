# 4. PropTypes and defaultProps
Created Sunday 06 September 2020

#### Why
The props we use in React components are supposed to be of a certain type. But this is not indicated anywhere. This can cause wrong type of props to be received by the rendering component. To avoid this, we use the `prop-types` npm library, which lets us created `console` level error checks for the type of props received.

Note that we could use `TypeScript` if we wanted to use a type for variables, but it is an overhead to use `TypeScript`. `prop-types` is a lighter solution for specifying types.

Also, sometimes we are supposed to receive a prop but it is not passed, this can break our component because of `undefined`. To get rid of this, we can specify default values of the props, so errors like this are caught.

#### How
`propTypes` is a library.
`defaultProps` are already included in `create-react-app` projects.

It is to be noted that we are specifying props that are being received, not being sent. This is because sent ones are already known - they may be a prop or created just here.

Also, note that for both `propTypes` and `defaultProps`, it does not matter if we use a props object or de-structure them. Just make sure the names of the receiving props are named correctly during specification.

During specification, both values are lowercase, follow component name and are plural. Like so:
```jsx
MyComponent.propTypes = { // lowercase start
	name: PropTypes.string // capital here, coz it's a constant
}
MyComponent.defaultProps = {} //lowercase start
```

#### What
###### PropTypes
To use `propTypes`, first install it in the project (`npm i prop-types`) and import it in the *receiving* component.
```jsx
import PropTypes from 'prop-types'; // for using type constants, so capital
```

To specify types, the syntax is:
```jsx
// receiving component file

const MyReceivingComponent = () => { ... } // component defintion
// may be class or functional component

MyReceivingComponent.propTypes = { // lowercase propTypes
	name: PropTypes.string, // optional string
	obj: PropTypes.object, // object
	age: PropTypes.number, // optional number
	rarr: PropTypes.array, // optional array
	action: PropTypes.func.isRequired, // function and always required

	numArr: PropTypes.arrayOf(PropTypes.number), // array of numbers
	enumm: PropTypes.oneOf(['News', 'Photos', 'Game']) // enum - one of values
	oneType: PropTypes.oneOfType([ // one of types
		PropTypes.string,
		PropTypes.number
	])
	optionalShape: PropTypes.shape({ // object and it's minimalist shape. Can be nested. More name-value pairs could be added.
		color: PropTypes.string,
		fontSize: PropTypes.number
	})
	exactShape: PropTypes.exact({ // exact object, cannot have extra/less name value pairs
		name: PropTypes.string,
		fontSize: PropTypes.number,
		id: PropTypes.string,
	})
	anyTypeProp: PropTypes.any, // any data type is acceptable

	element: PropTypes.element, // a React element
	specificElement: PropTypes.MyComponent, // a React element of type MyComponent
	renderableNode: PropTypes.node, // anything that may be rendered directly

	genericType: PropTypes.instanceOf(ClassName), // prop is an object of type ClassName
}
```
- `isRequired` for `propTypes` entries is appended to the last to indicate the prop should always be received, i.e. it cannot be blank.
- `isRequired` and default value are mutually exclusive - If a prop is tagged `isRequired`, a default value for it makes no sense, and should be omitted. If it's not `isRequired`, a default value should always be specified.
- Only `PropTypes.bool` (`boolean`) and `PropTypes.func` (`function`) are named unusually.
- We can combine the types of values and make complex types using `PropType`.
- For more types, see https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes

---
###### defaultProps
The syntax for this is:
```jsx
// MyReceivingComponent is defined, class or functional component

MyReceivingComponent.defaultProps = {
	prop1: "Default val",
	propObject: {}, // an empty object
}
```

That' all.

#### Single child for wrapper
To specify that a single component is wrapper around our component (see [3._Wrapper_components](3._Wrapper_components.md)), do this:
```jsx
MyComponent.propTypes = {
	children: propTypes.element.isRequired,
}
```