<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Load Data into DynamoDB

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-databases-dynamodb)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## Load Data into a DynamoDB Table

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-dynamodb_b481c730)

---

## Introducing Today's Project!

### What is Amazon DynamoDB?

Amazon DynamoDB is a fully managed NoSQL database service provided by AWS. It’s designed for fast, predictable performance and seamless scalability — without you having to manage servers, storage, or database administration.

### How I used Amazon DynamoDB in this project

In today’s project, I used Amazon DynamoDB to store and manage application data in a fast and scalable way without needing to set up or manage any servers.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how easy and fast it was to set up and interact with DynamoDB using AWS CloudShell and the CLI — there was no need to configure servers or databases manually.

### This project took me...

This project took me 1 hour. 

---

## Create a DynamoDB table

Data in a DynamoDB table is organized into:

Tables → top-level containers for data.

Items → individual records (like rows in SQL).

Attributes → data fields within an item (like columns).

Primary key → uniquely identifies each item (either partition key or partition + sort key).

Partitions → physical storage units where items are distributed based on the partition key’s hash value.

In DynamoDB, an attribute is like a piece of data about an item. In this case, our item is Nikko and the attribute is the number of projects Nikko completed.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-dynamodb_a3cefee0)

---

## Read and Write Capacity

Read Capacity Units (RCUs) and Write Capacity Units (WCUs) in DynamoDB define how much throughput your table can handle:

1 RCU = one strongly consistent read per second for an item up to 4 KB, or two eventually consistent reads per second.

1 WCU = one write per second for an item up to 1 KB.

They determine the speed and cost of reading/writing data in provisioned mode.

DynamoDB Free Tier includes:

25 GB of storage

25 RCUs and 25 WCUs (provisioned mode)

2.5 million stream read requests per month

1 GB data transfer out per month

Charges apply once these limits are exceeded.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-dynamodb_ef47dd8f)

---

## Using CLI and CloudShell

AWS CloudShell is shell in your AWS Management Console, which means it's a space for you to run code. The awesome thing about AWS CloudShell is that it already has AWS CLI pre-installed.

AWS CLI (Command Line Interface) is a software that lets you create, delete and update AWS resources with commands instead of clicking through your console.

aws dynamodb create-table \
    --table-name ContentCatalog \
    --attribute-definitions \
        AttributeName=Id,AttributeType=N \
    --key-schema \
        AttributeName=Id,KeyType=HASH \
    --provisioned-throughput \
        ReadCapacityUnits=1,WriteCapacityUnits=1 \
    --query "TableDescription.TableStatus"
aws dynamodb create-table \
    --table-name Forum \
    --attribute-definitions \
        AttributeName=Name,AttributeType=S \
    --key-schema \
        AttributeName=Name,KeyType=HASH \
    --provisioned-throughput \
        ReadCapacityUnits=1,WriteCapacityUnits=1 \
    --query "TableDescription.TableStatus"
aws dynamodb create-table \
    --table-name Post \
    --attribute-definitions \
        AttributeName=ForumName,AttributeType=S \
        AttributeName=Subject,AttributeType=S \
    --key-schema \
        AttributeName=ForumName,KeyType=HASH \
        AttributeName=Subject,KeyType=RANGE \
    --provisioned-throughput \
        ReadCapacityUnits=1,WriteCapacityUni

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-dynamodb_81e0258b)

---

## Loading Data with CLI

I ran a CLI command in AWS CloudShell:

aws dynamodb batch-write-item --request-items file://ContentCatalog.json

aws dynamodb batch-write-item --request-items file://Forum.json

aws dynamodb batch-write-item --request-items file://Post.json

aws dynamodb batch-write-item --request-items file://Comment.json


![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-dynamodb_791c600b)

---

## Observing Item Attributes

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-dynamodb_b481c731)

Difficulty,Price, Projectcategory, Published, Title, URL

I checked another ContentCatalog item, which had a different set of attributes: ContentType, Price, Services, Title, URL, VideoType. 

---

## Benefits of DynamoDB

A benefit of DynamoDB over relational databases is flexibility, because  every item having their own unique set of attributes is a huge advantage when items in a table could look different from each other. For example, e-commerce sites and shopping carts need to store different types of products with different attributes in the same place.

Another benefit over relational databases is speed, because DynamoDB tables can use partition keys to split up a table and quickly find the items they're looking for. Relational databases have to scan through the entire table to find data, which can slow down performance.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-databases-dynamodb_b481c730)

---

---
