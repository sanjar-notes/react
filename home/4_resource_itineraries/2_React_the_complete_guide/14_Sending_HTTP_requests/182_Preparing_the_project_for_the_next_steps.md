# 182. Preparing the project for the next steps
Created Tuesday 19 July 2022

### Why
We have worked with `GET` requests. It's time to `POST` data to a backend.
The Star Wars API is a read-only API. We need something where we can submit data.

We'll be using Firebase. It provides a simple backend-app with a database through a REST API as one of it's features. It's free to use.


### How
1. Log in to Firebase
2. Create a project
3. Go to Build -> Realtime Database
4. Create a database and Start in "Test mode"
5. Copy the generates URL.

This URL can be used to communicate with the backend, and consequently read/write to the database.

Append a JSON file name after the last `/` of the URL. Example: `/movies.json`.
If this database node does not exist, it will be created.

Generated URL: https://react-http-88257-default-rtdb.asia-southeast1.firebasedatabase.app/movies.json