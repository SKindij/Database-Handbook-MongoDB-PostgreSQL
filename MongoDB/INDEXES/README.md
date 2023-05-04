# 📚 What is indexing?

## <a name="creating"></a>📖 Creating indexes
&ensp; **Indexes** are a powerful feature in MongoDB that help improve the performance of read operations (queries) in your database. 
They work similarly to the indexes found in a book, where you can quickly locate specific information rather than scanning through the entire content. 

&ensp; Basically, an **index** in MongoDB is a data structure that holds a smaller version of the data in our documents, along with a reference to the original document. 
**Indexes** can be created on one or more fields in a MongoDB collection. The default index that exists in every collection is the _id index, which ensures unique values for the _id field.

&ensp; To create an index on a field or fields, you can use the ``createIndex()`` method.\
To see which index is being used for a specific query, you can use the ``explain()`` method. 

## <a name="types"></a>📖 Index types
+ Single Field: Index based on a single field in the documents:
+ Compound: Index based on multiple fields in the documents:
+ Multikey: Index used when the indexed field contains an array of values:
+ Text: Index used to support text search queries on string content:
+ 2dsphere: Index used to support geospatial queries on spherical data:
+ 2d: Index used to support geospatial queries on planar data:

> ```javascript
>  // if you frequently query collection by name,
>  // create single-field index on "name" field to improve performance of those queries
>    db.witcherCharacters.createIndex({ name: 1 });
>  
>  // if you frequently query by both "profession" and "status" fields
>  // create compound index on "profession" and "status" fields
>    db.witcherCharacters.createIndex({ profession: 1, status: 1 });
>  
>  // suppose "witcherMonsters" has large number of docs and each document has array of "tags"
>  // if you frequently query based on those tags, and array may contain multiple values
>    db.witcherMonsters.createIndex({ tags: 1 });
>
>  // suppose "witcherBooks" has large number of documents,
>  // you frequently search for books based on keywords in "description" field
>    db.witcherBooks.createIndex({ description: 'text' });
>
>  // suppose each document has "location" field containing latitude and longitude of monster
>  // you frequently query for monsters within certain distance of a given point
>    db.witcherMonsters.createIndex({ location: '2dsphere' });
>
>  // suppose each document has "location" field containing x and y coordinates of character
>  // tou frequently query for characters within certain distance of a given point
>    db.witcherCharacters.createIndex({ location: '2d' });
> ```
> > _It’s important to choose right type of index for queries you will be running on your MongoDB collection._

## <a name="optimization"></a>📖 Query Optimization
&ensp; 


&ensp; 



