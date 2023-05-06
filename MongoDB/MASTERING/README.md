# 📚 Mastering MongoDB
&ensp; They aim to help you manage, interact, and visualize your data to make development tasks quicker and easier.

## <a name="tools"></a>📖 Developer Tools

### MongoDB Shell (mongo)
&ensp; It is a **command-line interface** (CLI) that allows you to interact with a MongoDB instance. It is still a popular tool among developers, especially for tasks like querying data, CRUD operations and performing administrative tasks.\
&ensp; ``mongo [options] [db address]``

### MongoDB Compass
&ensp; It is a **graphical user interface** (GUI) that simplifies the process of managing your MongoDB data. With [Compass](https://www.mongodb.com/products/compass), you can visually explore and interact with your data, modify and sort documents, create indexes, and validate data schemas for better data governance.

### VS Code Extension
&ensp; It provides a convenient and powerful way to work with MongoDB databases directly from [VS Code](https://marketplace.visualstudio.com/items?itemName=mongodb.mongodb-vscode). This extension allows you to effortlessly manage your MongoDB databases, perform CRUD operations, and visualize your data schema within the VS Code environment. 
* Once connected, you can explore your databases and collections directly from within the VS Code Explorer panel.
* It provides a rich query editor that allows you to build and run queries against your MongoDB databases.
* You can add, update, and delete documents directly from within VS Code.
* It provides functionality for exporting and importing data to and from your MongoDB databases.
* It provides IntelliSense support for working with MongoDB, making it easier to write code that interacts with your databases.

### MongoDB Atlas
&ensp; It is a fully-managed **cloud-based database platform** offering the best of MongoDB. Its intuitive interface provides an effortless deployment experience, automated backups, self-healing recovery, and many other features that make [Atlas](https://www.mongodb.com/atlas/database) an ideal choice for database management.

### Connectors APIs and Drivers
&ensp; MongoDB offers a variety of APIs and native drivers for numerous programming languages, enabling developers to build applications using their preferred languages. The most popular of these include: [Node.js Driver](https://www.mongodb.com/docs/drivers/node/current/), [Python Driver (Pymongo)](https://www.mongodb.com/docs/drivers/pymongo/), [C# Driver](https://www.mongodb.com/docs/drivers/csharp/current/).\
&ensp; With language drivers, you can perform various CRUD operations, manage authentication, and handle connections with the database effectively without worrying about low-level details.

&ensp; With a suitable driver installed, you can interact with MongoDB using the idiomatic style of your programming language. The driver simplifies your code and boosts productivity, as it handles the communication between your application and the MongoDB server.\
&ensp; The documentation will help you set up the driver, establish a connection, and perform various database operations in your preferred programming language. Remember to always use the latest version of language drivers to ensure compatibility with new MongoDB features and improve overall performance.

&ensp; MongoDB **Connectors** provide the integration between your application and the MongoDB database, allowing your applications to interact with the data stored in MongoDB. These connectors enable you to use your preferred language, framework, or platform to communicate with MongoDB using native APIs or drivers.
+ BI Connector
  * it allows you to connect MongoDB to third-party tools like Tableau or PowerBI, enabling users to create visualizations, reports, and dashboards using data;
  * it translates incoming SQL queries into equivalent MongoDB queries, providing a seamless experience when working with your data.
+ [Kafka Connector](https://www.mongodb.com/docs/kafka-connector/current/source-connector/)
  * it lets you stream data between Apache Kafka and MongoDB, enabling you to build real-time, event-driven data pipelines that can process and analyze large volumes of data quickly;
  * you can use Kafka as the central event bus for your system and automatically persist the events in MongoDB as required.
+ [Connector for Spark](https://www.mongodb.com/docs/spark-connector/current/)
  * it enables you to use MongoDB as a data source or destination for Apache Spark, a powerful analytics engine designed for large-scale data processing;
  * you can leverage Spark’s advanced capabilities like machine learning and graph processing on your MongoDB data.

### Studio 3T (MongoChef GUI)

&ensp; **Robo 3T** (_formerly_ [Robomongo](https://robomongo.org/)) is a lightweight, open-source MongoDB management tool. It provides basic features like connecting to a MongoDB instance, managing databases, collections, and performing CRUD operations.

&ensp; **Studio 3T** is a powerful, feature-rich MongoDB management tool that provides a comprehensive set of tools and features for MongoDB management and development. [Studio 3T](https://studio3t.com/) offers advanced features such as IntelliShell, Query Code, and SQL Migration.

- - -

## <a name="transactions"></a>📖 Transactions
&ensp; They play a vital role in maintaining data consistency and integrity within a database. They represent a single unit of work that consists of multiple operations executed in a sequence.

### Overview
&ensp; MongoDB supports multi-document transactions, enabling you to perform multiple read and write operations across several documents within a single, atomic transaction. 
A transaction might involve several operations, for instance:
* Creating a new document
* Updating an existing document
* Deleting a document
* Reading documents

&ensp; The fundamental purpose of a transaction is to either execute all or none of its operations. This means that, in case any operation within the transaction fails, the entire transaction will be aborted, and the database will return to its initial state, thus ensuring data consistency.

&ensp; Transactions in MongoDB are essential to achieve the following ACID properties:
+ Atomicity: Ensures that either all the operations in the transaction are executed, or none are.
+ Consistency: Guarantees that, upon completing a transaction, the database remains in a consistent state.
+ Isolation: Secures that the operations within the transaction are isolated from other transactions being executed simultaneously.
+ Durability: Warrants that once a transaction is successfully completed, its effects will be stored persistently in the database.

### Usage
&ensp; To begin a transaction in MongoDB, you’ll need to obtain a session and then start the transaction using the startTransaction() method. After performing the necessary operations, you may commit the transaction to apply the changes to the database, or abort to discard the changes.

> Here are a few examples related to "The Witcher" universe:\
> Example 1: Creating transaction to add new Witcher and update their current location
> > ```javascript
> >  // start by creating new session
> >  // session will be used to group operations of our transaction
> >  const session = await mongoose.startSession();
> >    // this marks start of our atomic operation
> >    session.startTransaction();
> >  
> >  try {
> >    // create new Witcher object with desired properties 
> >      const newWitcher = new Witcher({
> >        name: 'Geralt of Rivia',
> >        age: 100,
> >        gender: 'Male'
> >      });
> >      // save 'newWitcher' to 'witchers' collection
> >   // session is passed as option to ensure that operation is performed within transaction
> >      const savedWitcher = await newWitcher.save({ session }); 
> >      // update locations collection
> >      const updatedLocation = await Location.findOneAndUpdate(
> >          // to find location document with name
> >          { name: 'Kaer Morhen' },
> >          // to add new ID to witchers array in location document
> >          { $push: { witchers: savedWitcher._id } },
> >          // ensure that we receive updated location document as result
> >          { new: true, session }
> >      ); 
> >     // if all operations are successful, we call this to commit transaction
> >     // this will persist all changes made within transaction to database
> >      await session.commitTransaction();
> >      // we call this to end session
> >      session.endSession();
> >      console.log('Successfully added new Witcher and updated their current location!');
> >  // if error occurs at any point within transaction, we catch it
> >  } catch (error) {
> >      // to roll back any changes made within transaction
> >      await session.abortTransaction();
> >      session.endSession();
> >      console.error('Error adding new Witcher and updating their current location:', error);
> >  }
> > ```

> Example 2: Creating a transaction to add new monster and deduct coins from Witcher's purse
> > ```javascript
> >  const session = await mongoose.startSession();
> >    session.startTransaction();
> >  
> >  try {
> >      const newMonster = new Monster({
> >          name: 'Striga',
> >          threatLevel: 'High',
> >          location: 'Vizima'
> >      });
> >      const savedMonster = await newMonster.save({ session });
> >      const witcher = await Witcher.findOneAndUpdate(
> >          { name: 'Geralt of Rivia' },
> >          { $inc: { coins: -500 } },
> >          { new: true, session }
> >      );
> >      await session.commitTransaction();
> >      session.endSession();
> >      console.log(`Successfully added new monster ${savedMonster.name} and deducted 500 coins from ${witcher.name}'s purse!`);
> >  } catch (error) {
> >      await session.abortTransaction();
> >      session.endSession();
> >      console.error('Error adding new monster and deducting coins:', error);
> >    }
> > ```

> Example 3: Creating a transaction to delete a Witcher and all of their associated contracts and payments
> > ```javascript
> >  const session = await mongoose.startSession();
> >    session.startTransaction();
> >  
> >  try {
> >      const witcher = await Witcher.findOne({ name: 'Eskel' }).session(session);
> >        await Contract.deleteMany({ witcher: witcher._id }).session(session);
> >        await Payment.deleteMany({ witcher: witcher._id }).session(session);
> >        await Witcher.findByIdAndDelete(witcher._id).session(session);
> >      await session.commitTransaction();
> >      session.endSession();
> >      console.log(`Successfully deleted Witcher ${witcher.name} and all of their associated contracts and payments!`);
> >  } catch (error) {
> >      await session.abortTransaction();
> >      session.endSession();
> >      console.error('Error deleting Witcher and associated contracts and payments:', error);
> >  }
> > ```

### Limitations
* They are available only in MongoDB versions 4.0 and above.
* They can cause performance overhead, especially for write-heavy workloads.
* In MongoDB clusters, transactions only support a maximum duration of 60 seconds.

&ensp; In summary, transactions are a powerful feature of MongoDB, ensuring data integrity, and consistency in the database. By understanding their usage and implications, you can effectively utilize them in your application according to your specific requirements.

- - -

## <a name="scaling"></a>📖 Scaling Strategies
&ensp;Scaling is crucial for maintaining high performance and availability of your database, especially as your application and its data grow.

### Horizontal Scaling
&ensp;It refers to the process of adding more servers to a system to share the workload evenly.

#### Sharding
&ensp; It is a method of spreading data across multiple servers, allowing MongoDB to scale out and manage large amounts of data. Sharding enables you to partition your data and distribute it across several machines, ensuring that no single machine is overwhelmed with data or queries. With the use of a shard key, MongoDB automatically distributes data across the multiple machines.

&ensp; Components of Sharding
+ Shard: 
  * single server or a replica set that stores a portion of the sharded data.
+ Config Server: 
  * server or a replica set that stores metadata about the sharded clusters. 
  * config server tracks which data is stored on which shard.
+ Query Router (mongos): 
  * server that routes the application queries to the appropriate shard based on the metadata obtained from the config server.


### Vertical Scaling
&ensp; It involves increasing the resources available on individual servers, such as CPU, memory, and storage. This can be done by adding more resources to existing servers or by upgrading to more powerful servers.

#### Replica Sets




