---
title: "Mongo Data Modeling"
date: 2021-03-04T00:18:07+05:30
lastmod: ""
draft: false
categories: ["Mongo", "design", "NoSQL"]
tags: ["Mongo", "NoSQL", "database", "design"]
resources:
  - name: "featured-image"
    src: "featured-image.jpg"
lightgallery: true
---

Designing mongo database is really fun in a way, it let's us understand the data relationships more intuitively. This is my opinionated stab at how to approach mongo datbase design for any application.

## Data Organisation

Documents are the basic unit of record in mongo. They are schema less and can have any type of fields and structure. Listed below are the most common terms.

1. Documents - schemaless documents
2. Collections - List of documents
3. Databases - List of collections

These are the things to consider while designing a database for an application.

## 1. Flexible Schema

1. Documents in a single collection do not need to have same set of fields.
2. Data type for a field can differ across documents within a collection

However in real world applications, we might need some sort of structure to the documents, and this could be achieved by having **[validation rules](https://docs.mongodb.com/manual/core/schema-validation/)** for `insert` and `update` operatons.

## 2. Document Structure

Designing data models for Mongo depends on the structure of the document and how the application represents relationships between data. Relations or related data can be handled in couple ways.

{{< admonition type=note >}}

- Embedded Data
- References

{{< /admonition >}}

### 2.1 Embedded Data

In this type of design, related data is stored within a single document structure.

```js
// schema
import mongoose from "mongoose";
const { Schema } = mongoose;

const users = new Schema({
  name: String,
  contact: {
    phone: {
      type: String,
      number: String,
    },
    email: String,
  },
  access: {
    level: Number,
    group: String,
  },
});
```

```js
// insert data
db.users.insert({
  name: "123abc",
  contact: {
    phone: {
      type: "cell",
      number: "123-456-7890",
    },
    email: "email@domain.com",
  },
  access: { level: 5, group: "dev" },
});

// access data in nested documents
db.users.find({ "contact.phone.number": "123-456-7890" });
```

{{< admonition type=note title="When to use" >}}

- Whenever there is a contains relationship between entities
- One to many relationships - where child documents are viewed in the context of parent documents

{{< /admonition >}}

{{< admonition type=tip title="Pros" >}}

- Better read performance and ability to retrieve related data in a single database operation.
- Embedded data models make it possible to update related data in a single atomic write operation.

{{< /admonition >}}

{{< admonition type=warning title="Gotchas" >}}

- [maximum size of the document 16 mb](https://docs.mongodb.com/manual/reference/limits/#bson-documents)
- [no more than 100 levels of nesting](https://docs.mongodb.com/manual/reference/limits/#Nested-Depth-for-BSON-Documents)

{{< /admonition >}}

### 2.2 References (Referential data)

In this type of design, the documents store the relationships between data by including links or references. There are two ways to store references.

{{< admonition type=note >}}

- Manual references
- DBRefs

{{< /admonition >}}

### 2.2.1 Manual References

[manual references](https://docs.mongodb.com/manual/reference/database-references/#document-references) where you save the \_id field of one document in another document as a reference. Then your application can run a second query to return the related data. These references are simple and sufficient for most use cases.

Consider the following operation to insert two documents, using the \_id field of the first document as a reference in the second document:

```js
original_id = ObjectId();

db.places.insert({
  _id: original_id,
  name: "Broadway Center",
  url: "bc.example.net",
});

db.people.insert({
  name: "Erin",
  places_id: original_id,
  url: "bc.example.net/Erin",
});
```

Then, when a query returns the document from the people collection you can, if needed, make a second query for the document referenced by the places_id field in the places collection.

<!-- #### When to use -->

{{< admonition type=note title="When to use" >}}

For nearly every case where you want to store a relationship between two documents, use manual references. The references are simple to create and your application can resolve references as needed.

{{< /admonition >}}

{{< admonition type=tip title="Pros" >}}

Straightforward to implement in application layer using some data mapper and application logic.

{{< /admonition >}}

{{< admonition type=warning title="Gotchas" >}}

The only limitation of manual linking is that these references do not convey the database and collection names. If you have documents in a single collection that relate to documents in more than one collection, you may need to consider using DBRefs.

{{< /admonition >}}

### 2.2.2 DBRefs

[dbrefs](https://docs.mongodb.com/manual/reference/database-references/#dbref-explanation) are references from one document to another using the value of the first document’s \_id field, collection name, and, optionally, its database name. By including these names, DBRefs allow documents located in multiple collections to be more easily linked with documents from a single collection.

```js
// DBRef documents resemble the following document:
{ "$ref" : <value>, "$id" : <value>, "$db" : <value> }
// Consider a document from a collection that stored a DBRef in a creator field:
{
  "_id" : ObjectId("5126bbf64aed4daf9e2ab771"),
  // .. application fields
  "creator" : {
    "$ref" : "creators",
    "$id" : ObjectId("5126bc054aed4daf9e2ab772"),
    "$db" : "users"
  }
}
```

The DBRef in this example points to a document in the creators collection of the users database that has ObjectId("5126bc054aed4daf9e2ab772") in its \_id field.

{{< admonition type=note >}}

The order of fields in the DBRef matters, and you must use the above sequence when using a DBRef.

{{< /admonition >}}

{{< admonition type=note title="When to use" >}}

In most cases you should use the manual reference method for connecting two or more related documents. However, if you need to reference documents from multiple collections, consider using DBRefs.

{{< /admonition >}}

{{< admonition type=tip title="Pros" >}}

Straightforward to implement in application layer using mongodb's transaction api.

{{< /admonition >}}

{{< admonition type=warning title="Gotchas" >}}

Be sure to use correct read and write concerns when creating a [transaction]

{{< /admonition >}}

### Summary

Lets review the concepts we've covered so far, we know how to organise data in mongo as documents. This is a good starting point for arriving at a database design for any product idea.

- The document are schemaless and we can enforce some structure by having schema validation for all insert and update operations.
- The documents can embed related data or have a reference to another document (multiple documents) depending on the size of the related data and frequency of operations.

I'm sure there are many important topics like Indexes, Transactions, Sharding, Capped Collections, Time to Live etc. In my next post, I would like to cover about the concepts like CRUD operations and Transactions.

### References:

1. https://docs.mongodb.com

<!-- [mongo dbref gist](https://gist.github.com/hastebrot/1170907/f6ce19225ede79e7cafc4f7ae85d2385d155a5f7)
[transaction](https://docs.mongodb.com/manual/core/transactions/#transactions-and-read-concern) -->
