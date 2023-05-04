# 📚 What is aggregation?
&ensp; It is the process of transforming data in MongoDB by grouping together documents and performing calculations on those groups. 
**Aggregation** is a powerful feature in MongoDB that allows you to analyze and manipulate data in various ways.

&ensp; MongoDB aggregation framework provides a set of operators to perform various operations on the data. 
  + The aggregation pipeline is a sequence of these operators that transform the documents as they pass through the pipeline. 
  + The pipeline consists of stages, and each stage performs a specific operation on the data.

## <a name="pipeline"></a>📖 Aggregation pipeline stages
+ ``$match`` - filters documents based on a specified condition:
  - ```javascript
      { $match: { <query> } } 
    ```
+ ``$group`` - groups documents by a specified field and calculates aggregate values for each group:
  - ```javascript
       { $group: 
          {
            _id: <expression>,
            <field1>: { <accumulator1> : <expression1> },
          }
       } 
    ```
+ ``$project`` - reshapes documents by including or excluding fields, creating computed fields, or renaming fields:
  - ```javascript
       { $project:
         {
            field1: <1 or 0>,
            field2: <1 or 0>,
         }
      } 
    ```
+ ``$sort`` - sorts documents based on one or more fields:
  - ```javascript
       { $sort: { field1: <sort order>, field2: <sort order>, ... } }
    ```
+ ``$skip`` - skips a specified number of documents in the pipeline:
  - ```javascript
       { $skip: <number> }
    ```
+ ``$limit`` - limits the number of documents returned by the pipeline:
  - ```javascript
       { $limit: <number> }
    ```

> ```javascript
>  // you can find all Witcher contracts that pay more than 1000 crowns
>  db.contracts.aggregate([ { $match : { reward : { $gt : 1000 } } }])
>
>  // you can find total number of Witcher contracts completed by each Witcher
>  db.contracts.aggregate([ { $group : { _id : "$witcher", num_contracts: { $sum: 1 } } } ])
>
>  // you can find only the name and gender of all Witchers
>  db.witchers.aggregate([ { $project : { name : 1, gender : 1 } } ])
>
>  // you can find all Witcher contracts sorted by reward amount in descending order
>  db.contracts.aggregate([ { $sort : { reward : -1 } } ])
>
>  // you can find all Witcher contracts except the first 10
>  db.contracts.aggregate([ { $skip : 10 } ])
>  
>  // you can find the 5 highest paying Witcher contracts
>  db.contracts.aggregate([
>     { $sort : { reward : -1 } },
>     { $limit : 5 }
>  ])
> ```

## <a name="operators"></a>📖 Aggregation operators
&ensp; They are used to perform various operations on the data as it passes through the pipeline. 
+ ``$sum`` - calculates the sum of a specified field in a group of documents:
+ ``$avg`` - calculates the average of a specified field in a group of documents:
+ ``$max`` - returns the maximum value of a specified field in a group of documents:
+ ``$min`` - returns the minimum value of a specified field in a group of documents:
+ ``$push`` - adds a value to an array:
+ ``$addToSet`` - adds a value to an array only if it does not already exist in the array:

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
