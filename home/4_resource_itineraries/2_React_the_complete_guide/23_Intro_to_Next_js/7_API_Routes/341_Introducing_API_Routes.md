# 341. Introducing API Routes
Created Monday 19 December 2022

## Why
For adding server-side code (via endpoints).


## How (does it work)
Obvious. Next.js runs on the server, so it's server side code. Adding more is easy.


## What (how to use API routes - syntax etc)
API endpoints can be made by creating one (`export default`) function per file (endpoint will correspond with file-name based routing). The function will be given access to request and response objects, as params.

1. To differentiate file-based routing for pages and server-side code files, endpoint files should be placed inside `pages/api`. 
2. They will be accessible by the URI `/api/remaining_path`. 
3. Just like with pages, API files can use square bracket notation in their name for dynamic route params.

- Next.js has implemented request-response code via the default `http` Node.js package. It does not use Express.
- API route code is not available to clients. Hence, we can do sensitive computations here like authentication etc. It stays and runs on the server only.
- Obviously, API endpoints don't work on React components or other UI aspects of the app.


- Client side code can use relative URL notation instead of absolute stuff like the domain name, since the UI server and web app (backend) server is the same.

Example
```js
// file `pages/api/new-meetup.js`, endpoint `/api/new-meetup`

export default myHandlerFunc(req, res) {
  if(req.method === "POST") {
    const data = req.body; // body of HTTP request

	const { title, image, address, description } = data;

	// pseudocode below, assume data validation is not needed.
	const id = generateUniqueId()l;
	db.addToTable('meetups', {id, title, image, image, address, description});
	res.send({message: "new meetup added", id: id});
	
  }
  else
    res.send({message: "Should be a POST request"}).status(404);
}
```
