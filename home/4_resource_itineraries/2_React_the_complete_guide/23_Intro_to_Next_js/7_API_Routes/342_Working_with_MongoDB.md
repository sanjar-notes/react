# 342. Working with MongoDB
Created Friday 23 December 2022

We'll use a MongoDB database. Instead of setting up a local instance, we'll use the MongoDB Atlas product, where we can set up a DB in the cloud and it offers a free tier that's sufficient for our use case here. 

1. Create an account
2. Create a project if none exist.
3. Create a database - select free plan, add a DB user, add current IP address if prompted.
4. Prepare to connect - install the Node package "mongodb" in the project. On the instance page (mongodb.com), click "Connect" and copy the string it presents. Also, make sure the current IP address has been added to the list.
5. Connect - In the API route file, import the `MongoClient` function from the "mongo" package, one of many functions.