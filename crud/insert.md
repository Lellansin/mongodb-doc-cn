# Insert Documents

This page provides examples of insert operations in MongoDB.

> CREATING A COLLECTION
>
> If the collection does not currently exist, insert operations will create the collection.

## Insert a Single Document

New in version 3.2.

[Collection.insertOne\(\)](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#insertOne)inserts a_single_[document](https://docs.mongodb.com/manual/core/document/#bson-document-format)into a collection.

The following example inserts a new document into the`inventory`collection. If the document does not specify an`_id`field, the Node.js driver adds the`_id`field with an ObjectId value to the new document. See[Insert Behavior](https://docs.mongodb.com/manual/tutorial/insert-documents/#write-op-insert-behavior).

```js
db.collection('inventory').insertOne({
  item: "canvas",
  qty: 100,
  tags: ["cotton"],
  size: { h: 28, w: 35.5, uom: "cm" }
})
.then(function(result) {
  // process result
})
```

[insertOne\(\)](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#insertOne)returns a promise that provides a`result`. The`result.insertedId`promise contains the`_id`of the newly inserted document.

To retrieve the document that you just inserted,[query the collection](https://docs.mongodb.com/manual/core/document/#document-query-filter):

```js
var cursor = db.collection('inventory').find({
  item: "canvas",
});
```

## Insert Multiple Documents

New in version 3.2.

[Collection.insertMany\(\)](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#insertMany)can insert_multiple_[documents](https://docs.mongodb.com/manual/core/document/#bson-document-format)into a collection. Pass an array of documents to the method.

The following example inserts three new documents into the`inventory`collection. If the documents do not specify an`_id`field, the Node.js driver adds the`_id`field with an ObjectId value to each document. See[Insert Behavior](https://docs.mongodb.com/manual/tutorial/insert-documents/#write-op-insert-behavior).

```js
db.collection('inventory').insertMany([
  { item: "journal",
    qty: 25,
    tags: ["blank", "red"],
    size: { h: 14, w: 21, uom: "cm" }},
  { item: "mat",
    qty: 85,
    tags: ["gray"],
    size: { h: 27.9, w: 35.5, uom: "cm" }},
  { item: "mousepad",
    qty: 25,
    tags: ["gel", "blue"],
    size: { h: 19, w: 22.85, uom: "cm" }}
])
.then(function(result) {
  // process result
})
```

[insertMany\(\)](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#insertMany)returns a promise that provides a`result`. The`result.insertedIds`field contains an array with the`_id`of each newly inserted document.

To retrieve the inserted documents,[query the collection](https://docs.mongodb.com/manual/tutorial/query-documents/#read-operations-query-document):

```js
var cursor = db.collection('inventory').find({});
```

## Insert Behavior

### Collection Creation

If the collection does not currently exist, insert operations will create the collection.

### `_id`Field

In MongoDB, each document stored in a collection requires a unique[\_id](https://docs.mongodb.com/manual/reference/glossary/#term-id)field that acts as a[primary key](https://docs.mongodb.com/manual/reference/glossary/#term-primary-key). If an inserted document omits the`_id`field, the MongoDB driver automatically generates an[ObjectId](https://docs.mongodb.com/manual/reference/bson-types/#objectid)for the`_id`field.

This also applies to documents inserted through update operations with[upsert: true](https://docs.mongodb.com/manual/reference/method/db.collection.update/#upsert-parameter).

### Atomicity

All write operations in MongoDB are atomic on the level of a single document. For more information on MongoDB and atomicity, see[Atomicity and Transactions](https://docs.mongodb.com/manual/core/write-operations-atomicity/)

### Write Acknowledgement

With write concerns, you can specify the level of acknowledgement requested from MongoDB for write operations. For details, see[Write Concern](https://docs.mongodb.com/manual/reference/write-concern/).

SEE ALSO

* [Collection.insertOne\(\)](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#insertOne)
* [Collection.insertMany\(\)](http://mongodb.github.io/node-mongodb-native/2.2/api/Collection.html#insertMany)
* [Additional Methods for Inserts](https://docs.mongodb.com/manual/reference/insert-methods/#additional-inserts)



