# 174. How to (Not) connect to a database
Created Monday 15 July 2022

##### Talking to a DB directly from client side app
- Browser-side apps don't, and shouldn't directly talk to databases.
- If an app does, the it's very badly written and highly unsecure app.
![](../../../../assets/Pasted%20image%2020220718044242.png)
But why?
- This is difficult to do (technically).
- All client side code is available to the user (i.e. via the browser dev tools, for example). Connecting *directly* to a database in a client app would, thus, expose database credentials to the outside world, which is not desirable and a huge security concern.
	Note: to know more about client-side code accessibility by the user, see [this](https://academind.com/tutorials/hide-javascript-code).
- Performance issues.

In short, it's not secure.

How do we then read/write data persistently in our client-side app (React app, for example)?

##### Back-end App
We employ a "back-end app" as a bridge between the client-app (React in this case) and the database. Essentially, it's a program running on the server, which is connected to the database program. 

Note: The database and back-end app may or may not be running on the same physical machine. It does not matter either way, it's irrelevant to the client-app.

![](../../../../assets/Pasted%20image%2020220718044924.png)

The back-end app has all the credentials of the database, and as it's code/data is not accessible to the client-side (in general, i.e. except what is allowed to be transmitted), there's no security issue.

OK, but how does the client-app read/write to the database?

Ignore authentication and authorization of the user (which is also a responsibility of the back-end) for now. The back-end app exposes an API (Application Programming Interface) which works according to HTTP, and is continuously listening for HTTP requests.

Finally, the client-side app makes HTTP requests to available APIs, via URLs for reading/writing data from/to the database. The client-side processes the response and populates/updates the UI accordingly in the browser.