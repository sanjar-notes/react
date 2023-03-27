# 176. Our starting App and backend
Created Monday 18 July 2022

### More about REST/GraphQL APIs(optional)
[Link](https://academind.com/tutorials/rest-vs-graphql)
- API here refers to HTTP based web APIs.
- About both:
	1. REST is an architectural style for web APIs.
	2. GraphQL is both a data manipulation language and a runtime for fulfilling queries made using the language.
- Both are ways to structure and work with web APIs.
- A backend app may use either or both. REST is the more prevalent and popular one, GraphQL is a younger

Similarities and differences
![](/assets/176_Our_starting_App_and_backend-image-1.png)

Essentially, difference between the two is the consumption style. Of course, the backend-app is also implemented differently. The query, in case of GraphQL, should abide by the GraphQL query specification.
![](/assets/176_Our_starting_App_and_backend-image-2.png)
![](/assets/176_Our_starting_App_and_backend-image-3.png)
![](/assets/176_Our_starting_App_and_backend-image-4.png)
![](/assets/176_Our_starting_App_and_backend-image-5.png)

When should one use REST, or GraphQL?
- **REST**
	- Pros:
		- Easy to use and implement.
	- Cons
		- Excessive data transmission, generally. e.g. you only need {name, picture} for posts, but you get entire objects.
		- Multiple requests may be needed by the client.
		- Client is somewhat bulkier, because multiple resources need to be tied together
- **GraphQL**
	- Pros
		- Data transported is minimal - more granular control over what is needed.
		- A single requests can fetch multiple resources.
	- Cons
		- A tad difficult to use and implement.
		- Client maybe bulkier due to GraphQL handling packages.

Of course, these are general characteristics, i.e. the decision depends on the needs of the client-side app.
