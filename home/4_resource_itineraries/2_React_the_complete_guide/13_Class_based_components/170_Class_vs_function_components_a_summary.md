# 170. Class vs function components: A summary
Created Monday 18 July 2022

- Building apps with class components alone is also fine.
- Functional components are the norm in modern React.
- It is fine to ignore class based components, except for Error boundaries.


### Differences between class and functional components:
Functional components:
1. Leaner
2. No use of the `this` keyword
3. Access multiple contexts easily

Class based components:
1. Verbose
2. Can't access contexts easily
3. Error boundaries need class based components.


### Recommendations from the instructor
1. Prefer functional components.
2. Use class based components if:
	1. If you prefer them
	2. The existing project codebase or convention involves class based components.
	3. For building Error boundaries.
	   