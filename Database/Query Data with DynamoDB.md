<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Query Data with DynamoDB

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-query)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## Query Data with DynamoDB

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-query_733d9399)

---

## Introducing Today's Project!

### What is Amazon DynamoDB?

 Amazon DynamoDB is a fully managed NoSQL database on AWS that provides fast, scalable, and serverless storage.

### How I used Amazon DynamoDB in this project

In today’s project, I used Amazon DynamoDB to store and manage project data efficiently.

Specifically:

Created a table (Projects) with a primary key.

Inserted sample items like project name, owner, and status using AWS CloudShell CLI.

Queried and scanned the table to retrieve specific information.

Tested CRUD operations (Create, Read, Update, Delete) to ensure proper functionality.

### One thing I didn't expect in this project was...

I expected to spend time managing servers or configuring infrastructure, but DynamoDB handled all of that automatically.

I was also surprised by the flexibility of the schema, allowing me to add or modify attributes without changing the table structure.

Querying and retrieving data was almost instant, even for multiple items.

### This project took me...

This project took me 1 hour.

---

## Querying DynamoDB Tables

A partition key in Amazon DynamoDB is the primary key attribute used to determine where an item is stored in the database.

A sort key in Amazon DynamoDB is the second part of a composite primary key that helps you organize and query related items within the same partition key.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-query_d105b0b0)

---

## Limits of Using DynamoDB

Missing or Incorrect Partition Key in the Query

DynamoDB requires the partition key in every query.

Understanding DynamoDB Basics

DynamoDB is a fully managed NoSQL database that provides fast performance, automatic scaling, and no server management.

It stores data as items (like rows) made up of attributes (like columns).

Hands-on Practice Using CloudShell

I used AWS CloudShell to create and manage a DynamoDB table through the AWS CLI.

I practiced CRUD operations — creating a table, inserting items, scanning data, and deleting the table.

Key Concepts Learned

Partition Key: Determines where an item is stored; every item must have this.

Sort Key: Allows multiple related items under one partition, sorted and easy to query.

Query Errors: Often caused by missing the partition key, wrong attribute names, or mismatched data types.

Unexpected Insight

I didn’t expect DynamoDB setup and operations to be this simple and fast — no manual server setup or scaling needed.

The schema flexibility made it easy to add attributes anytime.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-query_cb3e260c)

---

## Running Queries with CLI

aws dynamodb get-item \
    --table-name ContentCatalog \
    --key '{"Id":{"N":"202"}}' \
    --projection-expression "Title, ContentType, Services" \
    --return-consumed-capacity TOTAL


1️⃣ aws dynamodb get-item

This is the CLI command used to fetch a single item from a DynamoDB table.

It requires you to specify the table name and the primary key of the item you want.

2️⃣ --table-name ContentCatalog

Specifies the table you are querying: ContentCatalog.

3️⃣ --key '{"Id":{"N":"202"}}'

Defines the primary key of the item you want to fetch.

Here:

Id is the primary key attribute.

N indicates that the type of Id is a Number.

"202" is the value of the key for the item you want.

So DynamoDB will look for the item where Id = 202.

4️⃣ --projection-expression "Title, ContentType, Services"

This tells DynamoDB to return only specific attributes instead of the full item.

In this case, it will only return:

Title

ContentType

Services

This is useful to reduce read capacity usage and data transfer if you don’t need all attributes.

5️⃣ --return-consumed-capacity TOTAL

DynamoDB will return how much read capacity units (RCUs) were consumed by this operation.



![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-query_733d9399)

---

## Transactions

In Amazon DynamoDB, a transaction is a group of one or more operations that are executed as a single, all-or-nothing unit.

DynamoDB provides the aws dynamodb transact-write-items CLI command to perform multiple operations in a single atomic transaction.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-query_2f65f83e)

---

---
