---
title: "Mongo Query Primer"
date: 2021-03-10T18:10:47+05:30
lastmod: ""
draft: true
---

Mongo has been a primary database of choise with rise of MERN stack. Lets review the most frequently used query scenarios. To keep the things easier to follow, we will be using mongo shell client for the examples below.

### Creating a collection.

```shell
db.createCollection("my_collection")

```

### Insert a document to collection

```shell
# insert a document
db.my_collection.insertOne({
  "address": {
    "home": "123, Fourty Fifth avenue, Sector Six, 78900"
  },
})
```

### Update a document in collection

```shell

```

### Read a document from collection

```shell
# find all the documents in the collection
db.my_collection.find()

```

### Delete a document from collection

```shell
# deletes a document by id
db.my_collection.deleteOne({
  _id: ObjectId("6048bc3e77ef7b067cb04173")
})
```

Now that we have a basic idea about how to use mongo, lets see how we could use the same for building a database for a product idea.
