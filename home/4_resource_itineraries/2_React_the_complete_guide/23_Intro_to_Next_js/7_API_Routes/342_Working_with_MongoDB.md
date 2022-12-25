# 342. Working with MongoDB
Created Friday 23 December 2022

We'll use a MongoDB database. Instead of setting up a local instance, we'll use the MongoDB Atlas product, where we can set up a DB in the cloud and it offers a free tier that's sufficient for our use case here. 

1. Create an account
2. Create a project if none exist.
3. Create a database - select free plan, add a DB user, add current IP address if prompted.
4. Prepare to connect - install the Node package "mongodb" in the project. On the instance page (mongodb.com), click "Connect" and copy the string it presents. Also, make sure the current IP address has been added to the list.
5. Connect - In the API route file, import the `MongoClient` function from the "mongo" package, one of many functions.
   
   
## Mongo DB notes
### 1. **Connect to the server**
First copy the skeleton link provided by MongoDB site/local database URL. We need to pass in username password separated by colon.

Connecting is an async operation, obviously.
```js
import { MongoClient } from 'mongo';

async function handler() {
	const username = "myUserName1233", password = "zyfsPassworrd";
	const client = await MongoClient.connect(`mongodb+srv://${username}:${password}@cluster0.somethinxyz.mongodb.net`);
	const db = client.db(); // sync op
}
```
### 2. **Access a collection (aka table)**. 
It's a synchronous operation. The collection will be created if it does not exist.
```js
// assuming db variable from above
const meetupCollection = db.collection("meetups");
```
### 3. Query/mutate a collection
All query/mutate ops are async, and may fail.
```js
const allRows = await myCollection.find().toArray(); // get all rows, with all their entities

const allRowsJustNames = await myCollection.find({}, {name: 1}).toArray(); // get all rows, only with 'name' entity

const selectedRow = await myCollection.find({}, {_id: value_here}); // get row with _id of value

const result = await myUsersCollection.insertOne({ name: 'Sanjar', country: 'IN' });
```
- The `.toArray()` is important (FIXME: but why?)
- MongoDB adds a `_id` property automatically to a new row (object). 
- A problem with `_id` value is not "JSON serializable". It's a good idea to convert the value to a string, using `.toString()` before using it (on the client or server side). It must be converted back to original type for interaction with MongoDB, however. This can be done using the `ObjectId(_id_as_string)` function provided by MongoDB.
### 4. Closing the connection
```js
client.close();
```
(FIXME - is this an async operation? It doesn't matter on client side code, anyway)

Note
1. `mongo` package is meant to be run only on servers, and not the browser. So use it only inside server side code - `getStaticProps`, `getServerSideProps`, API routes etc.