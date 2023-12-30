# 4. Route enums in React Native
Created Sat Dec 30, 2023 at 1:54 PM

## Why enums
Using literal values for navigation code is a bad idea, because:
1. There's scope for typos
2. Even if there are no typos, one has to do "complete" testing to make sure everything works
3. Refactoring is hard in the future.
4. No auto-complete, too many manual lookups. Also, scope for error.

So, in addition to route markup (of navigators and screens), one should maintain a large POJO of just literals. And use this enum in navigation and initialRoute props.

## About nesting
1. Try to keep nesting to a minimum. Feature wise unrelated screens on the same navigator are fine, instead of feature based nested navigators. 
2. Of course, if the stack navigator is of a different type, then a dedicated navigator in a file of its own is fine.

## Enum structure
In a routes enum structure, there are 3 goals - uniqueness of keys, minimize manual lookup and ease of use in app code.

1. For uniqueness - I mean uniqueness of navigable entities (screens). create a linear object with keys and values identical. or Better, create variables one below the other, with name and value identical. In both cases, the editor will let you know about duplicates
2. Minimize manual lookup: first of all, what lookups are we talking about in a route structure? Parent and children are two possibilities right. Those are two pieces of data.  
	1. We know the self entity (whose parent or child we're finding) but still represent it to make sure we always use the same terminal key for navigation. `ROUTES.x.y.....screen`
	2. The value of this key will be an object  as we'll be creating an object here (2 pieces of data already). So keys are `screen`, `stackName`, `stack`.
	3. `base` key - Additionally if the entity is a navigator, add a `base` string, for use in `initialRouteName` in the markup of the same navigator. So if base changes, we only have to change this enum file. Don't use `base` in app code.
	4. `base` key - for simple screens, this key should be absent. Appearing/not-appearing in auto-complete is also helpful to check if current path is a simple screen or not. Lookup avoided.
3. Ease of usage - for usage with autocompletion we need an object (array won't do), so make the exported structure is a single object, and it uses the unique keys we created.

Con (not really): person has to check `stack`, `screen` and `navigator` below when a new screen is added. But that's a localized one time effort. Much better each member of the team having to do a lookup of the tree for each .navigate they do.

Idea example:
```js
// any navigable thing - be it navigator or screen
// linear object - for global uniqueness, and future refactorablity
// or one variable declaration at a line (uniquess should be identified)
//
// Note: don't export, only for unqiueness
const ENTITIES = {
  entity1: 'entity1',
};
// OR (better, avoid [] and . in ROUTES)
const ENTITY1 = 'entity1';
const ENTITY2 = 'entity2';


// potentially nested objected
// all right side values will be an entity
export const ROUTES = {
  [ENTITY1]: {
    // optional
    screen: [ENTITY1], // self. always there. Be it screen or navigator. Ik, duplicate, but can't do anything here. And dynamic generation will break autocompletion
    stackName: "", // parent stack navigator
    
    stack: {}, // own stack (children)
    // (below), value is an entity from inside `stack` that is the preferred stack screen
    // will not show up in autocomplete, indicating simple screen
    // we avoided a manual lookup
    base: '', // present only if `stack` is absent. I am a simple screen.
  },
};
```

Real example:
```js
// lowercase is fine too, since we're not exporting these
// Logged in?
const PUBLIC = "PUBLIC";
const PRIVATE = "PRIVATE";

// Cars
const CARS = "CARS";
const MY_CARS = "CARS";
const INCOMPLETE_DRIVES = "INCOMPLETE_DRIVES";
const ACTIVATE_CAR = "ACTIVATE_CAR";

// Profile
const PROFILE = "PROFILE";
const MY_PROFILE = "MY_PROFILE";
const MY_DETAILS = "MY_DETAILS";
const DRIVER_HANDBOOK = "DRIVER_HANDBOOK";

// Login
const LOGIN = "LOGIN";
const PASSWORD = "PASSWORD";
const FORGOT_PASSWORD = "FORGOT_PASSWORD";
const RESET_PASSWORD = "RESET_PASSWORD";
const MFA = "MFA";

const ROUTES = {
  [PRIVATE]: {
    [CARS]: {
      screen: [CARS], // screen (actually a navigator)
      stackName: [PRIVATE], // parent stack
      stack: {
        [MY_CARS]: {
          screen: [MY_CARS], // a simple screen this time (leaf)
          stackName: [CARS],
        },
        [INCOMPLETE_DRIVES]: {
          screen: [INCOMPLETE_DRIVES],
          stackName: [CARS],
        },
        [ACTIVATE_CAR]: {
          screen: [ACTIVATE_CAR],
          stackName: [CARS],
        },
      },
      base: [MY_CARS],
    },
    [PROFILE]: {
      // self properties
      screen: [PROFILE], // screen (actually a navigator)
      stackName: [PRIVATE], // parent stack

      // nested stack
      stack: {
        [MY_PROFILE]: {
          // same structure - parent stack, screen
          screen: [MY_PROFILE],
          stackName: [PROFILE],
        },
        [MY_DETAILS]: {
          screen: [MY_DETAILS],
          stackName: [PROFILE],
        },
        [DRIVER_HANDBOOK]: {
          screen: [DRIVER_HANDBOOK],
          stackName: [PROFILE],
        },
      },
      base: [MY_PROFILE],
    },
  },
  [PUBLIC]: {
    [LOGIN]: {
      screen: [LOGIN],
      stackName: [PUBLIC],
      // stack, base both missing for simple screen
    },
    [PASSWORD]: {
      screen: [PASSWORD],
      stackName: [PUBLIC],
    },
    [FORGOT_PASSWORD]: {
      screen: [FORGOT_PASSWORD],
      stackName: [PUBLIC],
    },
    [RESET_PASSWORD]: {
      screen: [RESET_PASSWORD],
      stackName: [PUBLIC],
    },
    [MFA]: {
      screen: [MFA],
      stackName: [PUBLIC],
    },
  },
};
```

## Conclusion
BTW, use these enums in the markup. I spoke about markup first since it's build in to React navigation, but markup according to me comes after enum is ready.