# 149. Using the useEffect hook
Created Saturday 01 July 2022

I have two things that are not clear to me:
1. When to use useEffect, exactly? The author used useEffect to apply styles to a component. If I keep thinking "useEffects are used for side-effects", how am I going to be sure when to use it. Need a better understanding of when to use useEffect. FIXME: when to use useEffect
2. How does state (and context) work for the descendant components? By this, I mean what happens to state of the descendant component when the parent's state changes, does their `useState` statement run again, or is anything preserved? This is really confusing for me. Example: There was a descendant using a context, and the context changed. I had a `console.log` in this component to monitor re-renders, but it never ran after the first time, which is strange since the context changed, and all descendants should be re-render. Does re-render not mean that the component function/file is ran again? FIXME: how do descendant re-renders work?

Answers
1. *TBD*
2. Okay here are the observations:
	1. Files are never re-run on render. Yeah, it doesn't make sense.
	2. Component functions are run again on re-render (i.e. of course, due to state change in relevant component/ancestor)
	3. Hooks are NOT run again, even if the re-render is caused by an ancestor.
	This means that a de-hooked copy of the function is kept in memory at all times.