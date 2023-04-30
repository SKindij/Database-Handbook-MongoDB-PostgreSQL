# 📚 Introduction to MongoDB

## 📖 What is MongoDB?
&ensp; It is a NoSQL (non-relational) document-oriented database. It was first released in 2009 and is developed by MongoDB Inc. MongoDB stores data in flexible, JSON-like documents, which makes it easy to store and retrieve data. It is used by many large organizations, such as Cisco, eBay, and SAP.\
&ensp; It is designed to be scalable and flexible, making it a popular choice for handling large amounts of data. It also supports many features, such as indexing, replication, and sharding, which make it a robust database solution.\
&ensp; One of the unique features of MongoDB is its ability to store data in a flexible schema. Unlike traditional relational databases, MongoDB does not enforce a rigid schema, which means you can add or remove fields to a document as needed. This makes it easier to work with data that may not have a fixed structure.

## 📖 Advantages of using MongoDB
+ It is very flexible, making it easier to work with data that may not have a fixed structure. This means that you can easily store data in a way that makes sense for your application.
+ It is designed to be scalable, which means you can easily add more servers to handle larger amounts of data. It also supports sharding, which allows you to distribute data across multiple servers.
+ Document-based data model and indexing features make it a high-performance database. It can handle large amounts of data and provide fast query response times.
+ It supports a rich query language that allows you to easily retrieve and manipulate data. It also supports aggregation, which allows you to perform complex data analysis.
+ MongoDB supports replication, which means you can have multiple copies of your data for increased availability and durability.
+ Large and active community of users and developers. There are many resources available to help you learn and use the database.

## 📖 Key concepts and terminology
+ Documents: 
  * MongoDB stores data in documents, which are similar to JSON objects. 
  * Document is a set of key-value pairs, where each key represents a field in the document and the corresponding value represents the data stored in that field.
+ Collections: 
  * It is a group of related documents in MongoDB. 
  * Collections are similar to tables in relational databases, but unlike tables, they do not enforce a fixed schema.
+ Indexes: 
  * They help to speed up queries by providing efficient access to data.
  * They are similar to indexes in relational databases, but they work differently in MongoDB. 
  * MongoDB supports several types of indexes, including single-field indexes, compound indexes, and geospatial indexes.
+ Aggregation: 
  * It allows you to perform complex data analysis by grouping, filtering, and transforming data in a collection. 
  * Aggregation pipelines consist of multiple stages, each of which performs a specific operation on the data.
+ Sharding: 
  * It is a method for distributing data across multiple servers in MongoDB. 
  * It allows you to scale horizontally by adding more servers to handle increased load.
+ Replica sets: 
  * It is a group of MongoDB servers that work together to provide high availability and data redundancy. 
  * It consists of one primary server and one or more secondary servers, which replicate data from the primary server.
+ GridFS: 
  * It is a specification for storing large files in MongoDB. 
  * It stores files in chunks, which are then stored as separate documents in a collection.

## 📖 Setting up a MongoDB environment
+ Install MongoDB: 
  * The first step in setting up a MongoDB environment is to download and install MongoDB. 
  * MongoDB provides installers for Windows, macOS, and Linux, which can be downloaded from the MongoDB website. 
  * Once you have downloaded the installer, follow the instructions to install MongoDB on your system.
+ Start the MongoDB server: 
  * After installing MongoDB, you need to start the MongoDB server. 
  * The server process is called mongod. 
  * You can start the server by running the mongod command in a terminal or command prompt window. 
  * By default, the MongoDB server runs on port 27017.
+ Connect to the MongoDB server: 
  * Once the MongoDB server is running, you can connect to it using the MongoDB shell. 
  * The MongoDB shell is a command-line interface that allows you to interact with the database. 
  * You can start the shell by running the mongo command in a terminal or command prompt window.
+ Create a database: 
  * To create a new database in MongoDB, you can use the ``use`` command. 
  * For example: ``use mydb``.
  * Note that the database is not actually created until you insert data into it.
+ Create a collection: 
  * To create a new collection in MongoDB, you can use the ``db.createCollection()`` method. 
  * For example: ``db.createCollection("users")``.
+ Insert data: 
  * To insert data into a MongoDB collection, you can use the ``insertOne()`` or ``insertMany()`` methods. 
  * For example: ``db.users.insertOne({ name: "John Doe", age: 30 })``.

## 📖 Basic CRUD Operations
+ Create: 
* To create a new document in a collection, you can use the ``insertOne()`` method.
* You can also use the ``insertMany()`` method to insert multiple documents at once.
+ Read: 
* To retrieve documents from a collection, you can use the ``find()`` method. 
* For example: ``db.users.find()``.
* You can also use the ``findOne()`` method to retrieve a single document that matches a specific query.
+ Update: 
* To update a document in a collection, you can use the ``updateOne()`` or ``updateMany()`` method. 
* For example: ``db.users.updateOne({ name: "John Doe" }, { $set: { age: 31 } })``.
+ Delete: 
* To delete a document from a collection, you can use the ``deleteOne()`` or ``deleteMany()`` method.
* For example: ``db.users.deleteOne({ name: "John Doe" })``.

As you become more familiar with the database, you can explore more advanced features such as aggregation, indexing, and sharding.
