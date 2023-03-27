# 267. What is Routing and Why
Created Saturday 27 August 2022

#### What is routing?
All projects made so far have the same URL for all their views (view states).
Sharing a URL to a certain view is not possible. This is bad because it increases manual work for the user.

What do we want - we want to have a set of URLs and their corresponding views, which remain in sync when the URL changes (either through the address bar by the user or programmatically by us).
![](assets/267_What_is_Routing_and_Why-image-1.png)

#### Why Client-Side Routing?
The needed flow, as mentioned above, is the default in a traditional multi-page application - where each URL has a corresponding HTML page, which is loaded when the URL changes. But this has the disadvantage of browser "reload" UX, which is the reason we're building an SPA in the first place.
![](assets/267_What_is_Routing_and_Why-image-2.png)

#### What we want
We want to add routing code to our SPA shell, so that it overrides the browser default (of loading a new page on URL change), and instead change the DOM to match the view when the URL changes.

In simple terms, we watch for the URL change or back/forward button events.

We do this via a library called React-Router.
![](assets/267_What_is_Routing_and_Why-image-3.png)
