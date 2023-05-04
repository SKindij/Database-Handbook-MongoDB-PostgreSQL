# 📚 What is indexing?

## <a name="creating"></a>📖 Creating indexes
&ensp; **Indexes** are a powerful feature in MongoDB that help improve the performance of read operations (queries) in your database. 
They work similarly to the indexes found in a book, where you can quickly locate specific information rather than scanning through the entire content. 

&ensp; Basically, an **index** in MongoDB is a data structure that holds a smaller version of the data in our documents, along with a reference to the original document. 
**Indexes** can be created on one or more fields in a MongoDB collection. The default index that exists in every collection is the _id index, which ensures unique values for the _id field.

&ensp; To create an index on a field or fields, you can use the ``createIndex()`` method.\
To see which index is being used for a specific query, you can use the ``explain()`` method. 

## <a name="types"></a>📖 Index types
+ Single Field: Index based on a single field in the documents.
+ Compound: Index based on multiple fields in the documents.
+ Multikey: Index used when the indexed field contains an array of values.
+ Text: Index used to support text search queries on string content.
+ 2dsphere: Index used to support geospatial queries on spherical data.
+ 2d: Index used to support geospatial queries on planar data.

> ```javascript
>  // create single-field index on "name" field
>  db.collection('witcherCharacters').createIndex({ name: 1 });
>  
>  // create compound index on "profession" and "status" fields
>  db.collection('witcherCharacters').createIndex({ profession: 1, status: 1 });
>  
>  // create geospatial index on "location" field
>  db.collection('witcherMonsters').createIndex({ location: '2dsphere' });
> ```
> > _It’s important to choose right type of index for queries you will be running on your MongoDB collection._

## <a name="optimization"></a>📖 Query Optimization
&ensp; 


&ensp; 



