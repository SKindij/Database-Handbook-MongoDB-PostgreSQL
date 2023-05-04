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

> Let's say you have a collection called "witcher_characters" with documents that look like this:
> > ```javascript
> >  {
> >    "_id": ObjectId("6092b8f30c3d3d3a78d1c573"),
> >    "name": "Geralt of Rivia",
> >    "race": "Witcher",
> >    "gender": "Male",
> >    "affiliations": ["The Witchers", "The School of the Wolf"]
> >  },
> >  {
> >    "_id": ObjectId("6092b8f30c3d3d3a78d1c574"),
> >    "name": "Yennefer of Vengerberg",
> >    "race": "Mage",
> >    "gender": "Female",
> >    "affiliations": ["The Lodge of Sorceresses"]
> >  },
> >  {
> >    "_id": ObjectId("6092b8f30c3d3d3a78d1c575"),
> >    "name": "Ciri",
> >    "race": "Human",
> >    "gender": "Female",
> >    "affiliations": ["The Witchers", "The School of the Wolf"]
> >  },
> >  {
> >    "_id": ObjectId("6092b8f30c3d3d3a78d1c576"),
> >    "name": "Triss Merigold",
> >    "race": "Mage",
> >    "gender": "Female",
> >    "affiliations": ["The Lodge of Sorceresses"]
> >  }
> > ```
> You want to group the characters by race and calculate the total number of characters for each race, and then sort the results in descending order by the total number of characters:
> > ```javascript
> >  db.witcher_characters.aggregate([
> >    {
> >      $group: {
> >        _id: "$race",
> >        count: { $sum: 1 }
> >      }
> >    },
> >    {
> >      $sort: { count: -1 }
> >    }
> >  ])
> > ```
> This pipeline would output the following results:
> > ```javascript
> >  { "_id" : "Mage", "count" : 2 }
> >  { "_id" : "Human", "count" : 1 }
> >  { "_id" : "Witcher", "count" : 1 }
> > ```
