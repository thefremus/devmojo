---
title: "Getting to grips with document databases"
date: 2023-04-11
author: "Fredrik Erasmus"
categories:
  - CosmosDB
tags:
  - NoSQL
  - Document Databases
---

![getting-to-grips-with-document-databases](img/getting-to-grips-with-document-databases.png)

# Getting to grips with document databases - case in point Cosmos DB

## A cosmic intro

So here I am after a very long period as a developer and I am covering Cosmos DB for my own learning purposes. Learning has to be fun right? What is the point if you cannot make it enjoyable? The post image was created using MidJourney with the command `/imagine a fun environment light hearted upbeat surreal cosmic world --ar 16:9`. 

## Digesting some content from Microsoft Learn

I asked some developers the other day whether they preferred using video based learning or text based learning and the majority indicated text books or text based resources as the preference. Video based learning has its advantages and disadvantages. So does text based material. Microsoft Learn falls into the text based learning category - even though there are videos interspersed between the content items. I have used Microsoft Learn in the past and it does give you something different when compared to a video from Udemy or YouTube. It comes down to developer preferences I guess. You can find on Microsoft Learn for a number of topics including [Cosmos DB](https://learn.microsoft.com/en-us/training/modules/explore-azure-cosmos-db/).

## What is a NoSQL database and how does it compare to relational database management systems?

What makes NoSQL (or CosmosDB) different from the traditional relational database management systems (RDBMS)? Most of my career has been spent using Microsoft SQL Server, some Postgres here, some MySQL (MariaDb) here and even some Oracle. So I am very much accustomed to the traditional frontend-with-an-api-connecting-to-a-database model. NoSQL is fundamentally different to relational databases - it is schema-less. With relational databases you cannot have a data model of any kind without a schema. A schema consists of defining your business entities in a table definition. The table definition defines your entity using columns (attributes). Each of your columns has an associated data type. The data types available to you can differ between RDBMS implementations. A table or entity can also be related to another entity through the definition of foreign keys. A foreign key is a reference from one table to another table using a primary key on the table being referenced. NoSQL on the other hand, in my mind at least, lets you store data as "documents" or as I see it JSON objects. It is, however, a very simplistic view of it. But I would like to know what sets the two approaches apart? What sets CosmosDB apart from something like SQL server? 

So the first thing that I noticed is the way CosmosDB appears to be architected - it works completely differently to SQL Server. The feeling I get is that it leverages cloud resources (Azure) in bigger (and better way??). A Cosmos DB can be spread across multiple regions - Cosmos DB handles the replication of your data internally across multiple regions. It all depends on how you setup your Cosmos DB to achieve consistency levels. The key takeaway for me here is the fact that CosmosDB leverages cloud resources in a manner that allows it to scale to higher levels. 

Talking about scale - the manner in which SQL Server and CosmosDB is scaled to meet performance demands is quite different. What does scaling a database mean? I guess you could ask the same question of an application running on a server somewhere. Scaling a database (or application) means the allocation of resources to improve its overall performance. Two key ways of describing scalability is to use the terms "horizontal scaling" and "vertical scaling". In my mind horizontal scaling means having a resource somewhere that is a duplicate of another resource in terms of resource allocation - things like CPU, RAM and storage space. The duplicated resource can then be configured to handle application load when the other resource runs at full capacity. Here I think of something like a load balancer. You can have it route resources to different VMs, for example, based on the resource consumption. If a VM is getting too much web traffic for instance, the load balancer can redirect to another VM to improve the responsiveness of your application. Most of the cloud providers allow you to scale automatically based on the need of your application. 

## Metaphorically speaking

I can think of scaling in metaphorical terms - imagine a slab of wood balancing on one leg in the middle. With horizontal scaling you can add more legs under the slab and spread them to make the weight distribution more even. The slab will balance more steadily with more legs spread under it - note that all the legs have the same dimensions. Horizontal scaling is almost like having the same leg under the slab, placed in the center, and you add more legs under the existing leg. I know its an arb metaphor. Horizontal scaling means adding more resources such as CPU or RAM to a single VM to make your app deal with additional load. You can visualize making the legs broader under the slab to make it bear more weight. But there is more still. 

## Consistency levels

Do you remember the consistency levels for a RDMS? Do you remember ACID? Atomicity, Consistency, Isolation and Durability. Consistency in a RDBMS refers to the state a database is in before and you write to it - or more specifically a transaction. Cosmos DB on the other hand is a distributed database and consistency refers to the tradeoffs between data consistency, latency and availability. My basic understanding is that when you, for example, write something to CosmosDB from your application you have to be explicit in how your application will achieve consistency with the data. In other words if I write a document (JSON) to Cosmos DB - how will I know when the data has been written. How long will it take for the data to consistent with all my other data? Cosmos DB provides several consistency levels.

1. Strong: This consistency level ensures that whenever you read data, you always get the most up-to-date version. It's similar to traditional databases but may cause slower performance and lower availability due to the time it takes to synchronize data across multiple nodes.
2. Bounded Staleness: This level allows some delay in getting the most recent data. You can set a limit on how old the data you read can be, either by the number of previous versions (K) or by time (t). This way, you trade some consistency for better performance and availability.
3. Session: With this level, each user or session is guaranteed to see its own changes immediately, but other users might see a delay. This is useful when it's important for a user to see their own updates right away, but other users can afford to wait.
4. Consistent Prefix: This level ensures that you always read data in the same order it was written, but you might not always get the most recent data. It prevents situations where you might see newer changes before older ones.
5. Eventual: This level prioritizes performance and availability over consistency. You might read outdated data, but the system is faster and more available because it doesn't wait for data to be synchronized across nodes. Eventually, all nodes will have the most recent data, but there can be temporary inconsistencies.

The consistency levels are a tradeoff between performance and availability. In other words the lower the level of consistency the better the performance. At the lower levels the availability of the data is not as immediate. If, for instance, you change data you might only see the updated changes at a later stage. 

## Resource hierarchy - CosmosDB

So the first important thing to note about CosmosDB is the nature of the Cosmos DB account. Because you can configure a Cosmos DB to be available across multiple regions the account acts as the root to all things Cosmos DB. If you think about the creation of VMs on Azure you will know (or not) that when you create a VM it is bound to a region. All the cloud providers use the concept of regions to denote where the resources are physically located. A region points to a physical data centre somewhere. There are other services on Azure that are not bound to a region - such as IAM. But many of the other services, like database services are locked to a region. Cosmos DB is different because of its distributed nature. You can specify which regions your Cosmos DB is available in by adding or removing regions. 

With Cosmos DB the starting point is the database account. A database account can have multiple databases. A database uses containers - they are used to store or contain your data. But it gets more complicated. 

A container in Cosmos DB is a collection of physical nodes. An example of a physical node would be a VM. One container can have multiple VMs, for instance, each with CPU, disk drive and RAM allocation. Cosmos DB acts as a type of load balancer - it distributes the load for you. There is nothing as a developer you need to know about the intricate details. It is, however, useful to conceptually understand how it all fits together. When you design your database you select a property in your JSON document as the partition key - it is a logical partition. Physical partitions is an internal mechanism used by Cosmos DB. 

A database can be seen as a namespace - you know like you have in C#. Its also worth noting that your Azure Cosmos DB account contains a unique DNS name.

> An Azure Cosmos DB container is the unit of scalability both for provisioned throughput and storage. A container is horizontally partitioned and then replicated across multiple regions. The items that you add to the container are automatically grouped into logical partitions, which are distributed across physical partitions, based on the partition key. The throughput on a container is evenly distributed across the physical partitions.

You can configure the request units for a container. Request units are the amount of reads, writes and queries. A cost is associated to each request unit.

Throughput, the number of request units, can be configured for each container, or at a database level. 

> Dedicated provisioned throughput mode: The throughput provisioned on a container is exclusively reserved for that container and it is backed by the SLAs.
> Shared provisioned throughput mode: These containers share the provisioned throughput with the other containers in the same database (excluding containers that have been configured with dedicated provisioned throughput). In other words, the provisioned throughput on the database is shared among all the “shared throughput” containers.

> A container is a schema-agnostic container of items. Items in a container can have arbitrary schemas. For example, an item that represents a person and an item that represents an automobile can be placed in the same container. By default, all items that you add to a container are automatically indexed without requiring explicit index or schema management.

> Depending on which API you use, an Azure Cosmos DB item can represent either a document in a collection, a row in a table, or a node or edge in a graph.

## The different models

Cosmos DB supports several models for storing data. 



