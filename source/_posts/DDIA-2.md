---
title: DDIA-2
date: 2020-10-06 23:04:19
categories: DDIA
tags: DDIA
---
# Data Models and Query Languages
### Birth of NoSQL
There are several driving forces of NoSQL

1. A need for greater **scalability** than relational databases can easily achieve, includ‐ ing **very large datasets or very high write throughput**
2. A widespread preference for **free and open source software** over commercial database products
3. **Specialized query operations** that are not well supported by the relational model
4. Frustration with the **restrictiveness of relational schemas**, and a desire for a more
dynamic and expressive data model

### The Object-Relational Mismatch
Most application development today is done in OO languages, which leads to the criticism of the SQL data model: if data is stored in relational tables, and awkward translation layer is required between the objects in the application code and the db model of rows, tables and columns. Called **Impedance mismatch**.

JSON representation has better locality(局部性) than the multi-table SQL schema. All the relevant information is in one place, and one query is sufficient.


### Many-to-One and Many-to-Many Relationships

In relational databases, it's normal to refer to rows in other tables by ID, because joins are easy. In document databases, joins are not needed for one-to-many tree structures, and support for joins is often weak.

If the database itself does not support joins, you have to emulate a join in application code by making multiple queries.

## Relational Versus Document Databases Today
* document data model are schema flexibility, bet‐ter performance due to locality, and that for some applications it is closer to the datastructures used by the application. 
* The relational model counters by providing bettersupport for joins, and many-to-one and many-to-many relationship


#### Which data model leads to simpler application code

If the data in your application has a document-like structure (tree of one-to-many relationships) then its a good idea to use a document model.

Document model has limitations, you cannot refer directly to a nested item within a document. As long as documents are not too deeply nested, not usually a problem.

if  your  application  does  use  many-to-many  relationships,  the  documentmodel becomes less appealing.

It is not posssible to say in general which data model leads to simpler application code; it depends on the relationships that exist between data items.


#### Schema flexibility in the document model
Document dbs are sometimes called schemaless, but that is misleading. The code usually assumes some kind of structure that is not enforced by the db. Schema-on-read is more accurate, compared to schema-on-write of relational dbs.

Schema changes have a bad reputation of being slow and requiring downtime for RDB.

### Data locality for queries
If application often needs to access the entire document there is a performance advantage to storage locality, having the data split across multiple table can take much longer.

Locality advantage only applies if you need large parts of the document at the same time. DB typically needs to load the entire document even if you only access a small portion, wasteful in large documents.