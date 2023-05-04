# 📚 What is aggregation?
&ensp; It is the process of transforming data in MongoDB by grouping together documents and performing calculations on those groups. 
**Aggregation** is a powerful feature in MongoDB that allows you to analyze and manipulate data in various ways.

&ensp; MongoDB aggregation framework provides a set of operators to perform various operations on the data. 
  + The aggregation pipeline is a sequence of these operators that transform the documents as they pass through the pipeline. 
  + The pipeline consists of stages, and each stage performs a specific operation on the data.

## <a name="pipeline"></a>📖 Aggregation pipeline stages
+ ``$match`` - filters documents based on a specified condition.
+ ``$group`` - groups documents by a specified field and calculates aggregate values for each group.
+ ``$project`` - reshapes documents by including or excluding fields, creating computed fields, or renaming fields.
+ ``$sort`` - sorts documents based on one or more fields.
+ ``$skip`` - skips a specified number of documents in the pipeline.
+ ``$limit`` - limits the number of documents returned by the pipeline.


## <a name="operators"></a>📖 Aggregation operators
&ensp; They are used to perform various operations on the data as it passes through the pipeline. 
+ ``$sum`` - calculates the sum of a specified field in a group of documents.
+ ``$avg`` - calculates the average of a specified field in a group of documents.
+ ``$max`` - returns the maximum value of a specified field in a group of documents.
+ ``$min`` - returns the minimum value of a specified field in a group of documents.
+ ``$push`` - adds a value to an array.
+ ``$addToSet`` - adds a value to an array only if it does not already exist in the array.

## <a name="sorting"></a>📖 Grouping and sorting data
+ ``$group`` stage is used to group documents by specified field and calculate aggregate values for each group. 
+  ``$sort`` stage can be used to sort the documents based on one or more fields.



## <a name="design"></a>📖 Schema Design
&ensp; It is an important consideration when using MongoDB. In general, you should design your schema based on how you plan to query the data. The aggregation pipeline can be used to reshape and transform data as needed for your queries.\
&ensp; Here are some tips for schema design:
* Denormalize data where appropriate to avoid the need for expensive joins.
* Use embedded documents and arrays to model relationships between data.
* Use indexes to improve query performance.
* Avoid using too many collections, as this can lead to performance issues.
