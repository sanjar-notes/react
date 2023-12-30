# 2. Routing enums web
Created Sat Dec 30, 2023 at 6:14 PM

## Why enums
Using literal values for navigation code is a bad idea, because:
1. There's scope for typos
2. Even if there are no typos, one has to do "complete" testing to make sure everything works
3. Refactoring is hard in the future.
4. No auto-complete, too many manual lookups. Also, scope for error.

So, in addition to route markup (of navigators and screens), one should maintain a large POJO of just literals. And use this enum in navigation and initialRoute props.

## About nesting
Nesting isn't an issue in web
In a routes enum structure, there are 3 goals - uniqueness of keys, minimize manual lookup and ease of use in app code.

1. For uniqueness - I mean uniqueness of navigable entities (pages). create a linear object with keys and values identical. or Better, create variables one below the other, with name and value identical. In both cases, the editor will let you know about duplicates.
2. Minimize manual lookup: first of all, what lookups are we talking about in a route structure? Parent and children are two possibilities right. Then there's self representation. And also, it's the web and path sections matter, so we should represent structure in such a way that we don't have to manipulate/concatenate stuff in the app code. 
	1. We'll use a single word (no `/`) key for a page or navigation link (like sidebar). We'll name the key `pathName` (not path, since path may indicate multiple words). This way, React Router local path is easy to specify (it is a single word).
	2. Full path to the page. We'll store it here itself. As `absolutePath`. This makes programmatic navigation easy. `ROUTES.x.y.....absolutePath`
	3. The value of this key will be an object  as we'll be creating an object here (2 pieces of data already). So keys are `pathName`, `absolutePath`.
	4. Store subpages (for navigation link) - as an object directory, follow same structure inside if there is a sub navigation link.
	5. `base` key - Additionally if the entity is a navigation link, add a `base` string, and specify `pathName` and `absolutePath` for use in `initialRouteName` in the markup. So if base changes, we only have to change this enum file. Don't use `base` in app code.
	6. `base` key - for simple single pages, this key should be absent. Appearing/not-appearing in auto-complete is also helpful to check if current path is a simple screen or not. Lookup avoided.
3. Ease of usage - for usage with autocompletion we need an object (array won't do), so make the exported structure is a single object, and it uses the unique keys we created.

Example:
```js
const PUBLIC = '/public'; // top level ones have /
const PRIVATE = '/private';

const WELCOME = '/welcome';
const LOGIN = '/login'; // top level ones have /
const FORGOT_PASSWORD = '/forgot-password'; // top level ones have /

const CARS_BASE_ROUTE = "/cars";
const PHYSICAL_CARS_PATH_NAME = "physical-cars"; // middle words, no /
const VIRTUAL_CARS_PATH_NAME = "virtual-cars";


export const ROUTES = {
  private: {
    pathName: [PRIVATE],
    absolutePath: `${PRIVATE}`,

    cars: {
      pathName: [CARS_BASE_ROUTE],
      absolutePath: `${PRIVATE}/${CARS_BASE_ROUTE}`,

	  physicalCars: {
	    pathName: [PHYSICAL_CARS_PATH_NAME],
	    absolutePath: `${PRIVATE}/${CARS_BASE_ROUTE}/${PHYSICAL_CARS_PATH_NAME}`,
	  },
	  virtualCars: {
	    pathName: [VIRTUAL_CARS_PATH_NAME],
	    absolutePath: `${PRIVATE}/${CARS_BASE_ROUTE}/${VIRTUAL_CARS_PATH_NAME}`,
	  }
    }
  },

  public: {
    pathName: [PUBLIC],
    absolutePath: `${PUBLIC}`,
    
    base: { // this will be used to represent preferred route in markup
      pathName: [WELCOME],
      absolutePath: `${PUBLIC}/${WELCOME}`,
    },

    welcome: {
      pathName: [WELCOME],
      absolutePath: `${PUBLIC}/${WELCOME}`,
    },
    login: {
      pathName: [LOGIN],
      absolutePath: `${PUBLIC}/${LOGIN}`,
    },
    forgotPassword: {
      pathName: [FORGOT_PASSWORD],
      absolutePath: `${PUBLIC}/${FORGOT_PASSWORD}`,
    }
  }
}
```

```jsx
  <Route>
	<Route
	  path={ROUTES.private.cars.absolutePath}
	  element={<MainApp />}
	>
	  <Route
		path={ROUTES.private.cars.physicalCars.pathName}
		element={<PhysicalCars />}
	  />
	  <Route
		path={ROUTES.private.cars.virtualCars.pathName}
		element={<VirtualCars />}
	  />
	</Route>
  </Route>
```