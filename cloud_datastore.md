# Cloud Datastore

- schemaless NoSQL DB
- ACID transactions
- strong/eventual consistency
- SQL-like quiries (GQL)
- 1MB/entity max size
- scales from zero to TBs
- multiple locataions
    - multi-regional
    - regional locataions
    - global points of presense

![alt](./images/cloud-datastore.png)

---
Each entity in a Datastore mode database has a key that uniquely identifies it. The key consists of the following components:
- The namespace of the entity, which allows for multitenancy
- The kind of the entity, which categorizes it for the purpose of queries
    - Each entity is of a particular kind, which categorizes the entity for the purpose of queries: for instance, a task list application might represent each task to complete with an entity of kind Task.
    - All kind names that begin with two underscores (__) are reserved and may not be used.
- An identifier for the individual entity, which can be either
    - a key name string
    - an integer numeric ID
    > Each entity has an identifier, assigned when the entity is created. Because it is part of the entity's key, the identifier is associated permanently with the entity and cannot be changed.
- An optional ancestor path locating the entity within the database hierarchy
---
Entities in a Datastore mode database form a hierarchically structured space similar to the directory structure of a file system. When you create an entity, you can optionally designate another entity as its parent; the new entity is a child of the parent entity. An entity without a parent is a root entity. The association between an entity and its parent is permanent, and cannot be changed once the entity is created. Datastore mode will never assign the same numeric ID to two entities with the same parent, or to two root entities (those without a parent).

An entity's parent, parent's parent, and so on recursively, are its ancestors; its children, children's children, and so on, are its descendants. The sequence of entities beginning with a root entity and proceeding from parent to child, leading to a given entity, constitute that entity's ancestor path. The complete key identifying the entity consists of a sequence of kind-identifier pairs specifying its ancestor path and terminating with those of the entity itself:
```
[User:alice, TaskList:default, Task:sampleTask]
```
---

## Indexes

Every Cloud Firestore in Datastore mode query computes its results using one or more indexes which contain entity keys in a sequence specified by the index's properties and, optionally, the entity's ancestors.
The indexes are updated to reflect any changes the application makes to its entities, so that the correct results of all queries are available with no further computation needed.

There are two types of indexes:
- Built-in indexes
    > By default, a Datastore mode database automatically predefines an index for each property of each entity kind. These single property indexes are suitable for simple types of queries.
- Composite indexes
    > Composite indexes index multiple property values per indexed entity. Composite indexes support complex queries and are defined in an index configuration file (index.yaml).

⚠️ joins and aggregate queries aren't supported within the Datastore mode query engine.

Composite indexes are viewable in the Indexes page of the GCP Console. You **cannot** use the GCP Console to create or update composite indexes.

An entity is included in the index only if it has an indexed value set for every property used in the index; if the index definition refers to a property for which the entity has no value, that entity will not appear in the index and hence will never be returned as a result for any query based on the index. The rows of an index table are sorted first by ancestor and then by property values, in the order specified in the index definition.

Index example:
```
indexes:
- kind: Task
  properties:
  - name: category
    direction: asc
  - name: priority
    direction: asc
  - name: created
    direction: asc
```
