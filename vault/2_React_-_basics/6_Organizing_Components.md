# 6. Organizing Components
Created Wednesday 09 September 2020

FIXME, write about - destructure props, smart vs dumb, headless components, styleProps/classProps, slots, propSets, dependencyInversion for generic buttons, core + common + page-components + pages directory, constants in enums, util functions in a dedicated file, custom hooks, component/page <--> Redux thunk <--> endpoint file arch.
#### Why
React is all about components and so it's normal to have more than 100 components in a project. Due to which organization becomes more important.

#### How
There are many ways to organize files:
1. Into `components` (specific components), `shared`(wrapper or shared components), `main` (integrating components) folders.
2. Have app's section wise folders and keep them heirarchical low levelled.

There are many ways. Just use what makes work on the app a pleasure.