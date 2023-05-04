📚 Schema design patterns
&ensp; It is an important consideration when using MongoDB. In general, you should design your schema based on how you plan to query the data. The aggregation pipeline can be used to reshape and transform data as needed for your queries.\
&ensp; Here are some tips for schema design:
* Denormalize data where appropriate to avoid the need for expensive joins.
* Use embedded documents and arrays to model relationships between data.
* Use indexes to improve query performance.
* Avoid using too many collections, as this can lead to performance issues.

## <a name="embedded"></a>📖 Embedded Data Model
* you can embed one or more documents inside another document, creating a nested or hierarchical structure;
* it is useful when you have one-to-many relationship between two entities and when you need to access related data in single query;

> in context of "Witcher" universe, you could embed contracts for each Witcher within Witcher document
> ```javascript
>  {
>     "_id": ObjectId("witcher_id"),
>     "name": "Geralt of Rivia",
>     "level": 60,
>     "contracts": [
>        {
>           "title": "The Beast of White Orchard",
>           "location": "White Orchard",
>           "reward": 100,
>           "witcher": "Geralt of Rivia"
>        },
>        {
>           "title": "The Merry Widow",
>           "location": "Novigrad",
>           "reward": 200,
>           "witcher": "Geralt of Rivia"
>        }
>     ]
>  }
> ```

## <a name=""></a>📖 
&ensp; 



## <a name=""></a>📖 
&ensp; 



## <a name=""></a>📖 
&ensp; 



