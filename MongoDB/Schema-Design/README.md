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

> _in context of "Witcher" universe, you could embed contracts for each Witcher within Witcher document_
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

## <a name="normalized"></a>📖 Normalized Data Model
* you can store related data in separate collections and reference them using unique identifiers, also known as foreign keys;
* useful when you have many-to-many relationship between two entities and when you need to update or delete related data without affecting original document; 

> _you could create separate collection for contracts and reference them in Witcher document using their ObjectId_
> ```javascript
>  // witchers collection
>  {
>     "_id": ObjectId("witcher_id"),
>     "name": "Geralt of Rivia",
>     "level": 60,
>     "contracts": [
>        ObjectId("contract_id_1"),
>        ObjectId("contract_id_2")
>     ]
>  }
>  
>  // contracts collection
>  {
>     "_id": ObjectId("contract_id_1"),
>     "title": "The Beast of White Orchard",
>     "location": "White Orchard",
>     "reward": 100,
>     "witcher": "Geralt of Rivia"
>  }
>  
>  {
>     "_id": ObjectId("contract_id_2"),
>     "title": "The Merry Widow",
>     "location": "Novigrad",
>     "reward": 200,
>     "witcher": "Geralt of Rivia"
>  }
> ```

## 📖 Hybrid Data Model
* you can combine the embedded and normalized data models to suit your specific needs;
* useful when you have complex data relationships and need to balance benefits of denormalization with drawbacks of data duplication; 

## <a name="subset"></a>📖 Subset Data Model
* you can store a subset of the data from one or more documents in a separate collection, typically for performance reasons; 
* this is useful when you have large or frequently accessed fields that are not needed for most queries;

> _you could create a separate collection for the combat statistics of each Witcher_
> ```javascript
>  // witchers collection
>  {
>     "_id": ObjectId("witcher_id"),
>     "name": "Geralt of Rivia",
>     "level": 60
>  }
>  
>  // witcher_combat_stats collection
>  {
>     "_id": ObjectId("witcher_id"),
>     "kills": 200,
>     "deaths": 0,
>     "victories": 20
>  }
> ```

## <a name="metadata"></a>📖 Metadata Data Model
* to store metadata about document, such as creation or modification timestamps, access control information, or auditing logs;
* useful when you need to track changes to a document over time, enforce security policies, or troubleshoot issues;

> _you could add a metadata field to each Witcher document_
> ```javascript
>  {
>     "_id": ObjectId("witcher_id"),
>     "name": "Geralt of Rivia",
>     "level": 60,
>     "metadata": {
>        "created_at": ISODate("2023-05-04T00:00:00.000Z"),
>        "updated_at": ISODate("2023-05-04T00:00:00.000Z"),
>        "created_by": "admin",
>        "updated_by": "admin",
>        "access_control": {
>           "read": ["admin", "user"],
>           "write": ["admin"]
>        },
>        "audit_log": [
>           {
>              "timestamp": ISODate("2023-05-04T00:00:00.000Z"),
>              "user": "admin",
>              "action": "create"
>           }
>        ]
>     }
>  }
> ```
