# 1. Normal styling
Created Monday 30 May 2022

Explain the following:
1. Styling problems in web apps - collisions, namespaces etc.
2. How styling should work in React, https://www.javatpoint.com/react-css
3. Research and add


FIXME: note that a mix of the following works well, and is intuitive to use.
1. Common global CSS file
2. Module CSS files
3. (optional) Tailwind - solves many collision problems, since many one-off styles (and these can be the majority) just stay outside of CSS files (global or module wise), and also don't collide.
4. (optional) SCSS - tailwind classes can be used within normal CSS blocks via mixins `@apply font-semibold`