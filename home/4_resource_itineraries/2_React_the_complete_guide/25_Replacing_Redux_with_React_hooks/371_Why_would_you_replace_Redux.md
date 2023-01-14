# 371. Why would you replace Redux
Created Saturday 14 January 2023

## Demo project for this section
[Demo project for this section](https://github.com/exemplar-codes/replacing-redux-with-context-and-hooks/)

This uses Redux because some data is needed by two different "pages", and using a global state is an easy and good solution.


## Why do it
1. Smaller bundle - don't have to bundle Redux. This may not be applicable to large apps, since their bundle is quite large anyway, and the reduction will be insignificant.
2. Learn less - maybe you don't want to learn an extra library and it's opinions.
3. Less boilerplate - Redux has some boilerplate and "opinions". This could be annoying to some developers.
4. Stay within core React - maybe you don't want to use 3rd party libraries as much as possible.
5. Explore - you simply want to explore how to manage global state without prop-drilling.

We are going to see two different approaches to do this. One of them is a good one, but the other may not be great for all use-cases.