---
title: System Design Basic
date: 2020-09-02 23:32:31
tags: System Design
categories: SystemDesign
---

### Scalability
Horizontal: scale by adding more servers into your pool of resources

Vertical scaling: scale by adding more power (CPU, RAM, Storage, etc.) to an existing server.

### Efficiency
Two standard measures of its efficiency are the:

1. response time (or latency) denotes the delay to obtain the first item
2. throughput (or bandwidth) which denotes the number of items delivered in a given time unit (e.g., a second). 


## Load Balancing
#### Key functions:

1. It helps to spread the traffic across a cluster of servers to improve responsiveness and availability of applications, websites or databases. 
2. keeps track of the status of all the resources while distributing requests. If a server is not available to take new requests or is not responding or has elevated error rate, LB will stop sending traffic to such a server.

### LB Algorithms

- Least Connection Method — This method directs traffic to the server with the fewest active connections. This approach is quite useful when there are a large number of persistent client connections which are unevenly distributed between the servers.
- Least Response Time Method — This algorithm directs traffic to the server with the fewest active connections and the lowest average response time.
- Least Bandwidth Method - This method selects the server that is currently serving the least amount of traffic measured in megabits per second (Mbps).
- Round Robin Method — This method cycles through a list of servers and sends each new request to the next server. When it reaches the end of the list, it starts over at the beginning. It is most useful when the servers are of equal specification and there are not many persistent connections.
- Weighted Round Robin Method — The weighted round-robin scheduling is designed to better handle servers with different processing capacities. Each server is assigned a weight (an integer value that indicates the processing capacity). Servers with higher weights receive new connections before those with less weights and servers with higher weights get more connections than those with less weights.
- IP Hash — Under this method, a hash of the IP address of the client is calculated to redirect the request to a server.


### Redundant Load Balancers
The load balancer can be a single point of failure; to overcome this, a second load balancer can be connected to the first to form a cluster. Each LB monitors the health of the other and, since both of them are equally capable of serving traffic and failure detection, in the event the main load balancer fails, the second load balancer takes over.


### L4 Load Balancer
Layer 4 load balancing (TCP layer)

L4 as the name suggests works on Layer4 (and Layer3) of the OSI model. When a client makes a request, it creates a TCP connection with the load balancer. The Load Balancer then uses the same TCP connection that the client created with it, to connect with one of the upstream servers.

The source and destination IP of each packet is changed by the load balancer using **NAT** (Network address translation).

When a response is received from the server, the same translation is performed again at the load balancer.
### L7 Load Balancer
L7 as the name suggests works on Layer7 (Layer6 and Layer5) of the OSI model. When a client makes a request, it creates a TCP connection with the load balancer. The Load Balancer then creates a new TCP connection with one of the upstream servers. Thus, there are 2 TCP connections as compared to 1 in a TCP/UDP passthrough L4 Load balancer.

Since we are at layer7, we are aware of the data in our request. This allows us to perform a variety of operations like

- Authentication — 401 if some header is not present
- Smart Routing — Route /payments call to a particular upstream
- TLS termination

Layer 7 load balancers look at the application layer to decide how to distribute requests. This can involve contents of the header, message, and cookies. Layer 7 load balancers terminate network traffic, reads the message, makes a load-balancing decision, then opens a connection to the selected server. For example, a layer 7 load balancer can direct video traffic to servers that host videos while directing more sensitive user billing traffic to security-hardened servers.



## Data Partitioning
### Partitioning Method
#### Horizontal partitioning
In this scheme, we put different rows into different tables. 

E.g. For example, if we are storing different places in a table, we can decide that locations with ZIP codes less than 10000 are stored in one table and places with ZIP codes greater than 10000 are stored in a separate table. This is also called a range based partitioning as we are storing different ranges of data in separate tables.

Cons: Need to choose the range of partition carefully or can cause unbalance traffic to tables 
#### Vertical Partitioning
we divide our data to store tables related to a specific feature in their own server. For example, if we are building Instagram like application - where we need to store data related to users, photos they upload, and people they follow - we can decide to place user profile information on one DB server, friend lists on another, and photos on a third server.

Cons: if our application experiences additional growth, then it may be necessary to further partition a feature specific DB across various servers (e.g. it would not be possible for a single server to handle all the metadata queries for 10 billion photos by 140 million users).
#### Directory Based Partitioning
A loosely coupled approach to work around issues mentioned in the above schemes is to create a lookup service which knows your current partitioning scheme and abstracts it away from the DB access code. So, to find out where a particular data entity resides, we query the directory server that holds the mapping between each tuple key to its DB server. This loosely coupled approach means we can perform tasks like adding servers to the DB pool or changing our partitioning scheme without having an impact on the application.

### Common Problems of Data Partitioning

### Joins
joins will not be performance efficient since data has to be compiled from multiple servers. 

A common workaround for this problem is to denormalize the database so that queries that previously required joins can be performed from a single table.  

### Referential integrity
trying to enforce data integrity constraints such as foreign keys in a partitioned database can be extremely difficult.

### Rebalancing 
There could be many reasons we have to change our partitioning scheme

## SQL VS NOSQL

### SQL
Relational databases store data in rows and columns. Each row contains all the information about one entity 

### NOSQL
* Key-Value Stores: Data is stored in an array of key-value pairs. Well-known key-value stores include **Redis**, Voldemort, and **Dynamo**.
* Document Databases: In these databases, data is stored in documents (instead of rows and columns in a table) and these documents are grouped together in collections. Document databases include the CouchDB and **MongoDB**.
* Wide-Column Databases: Instead of ‘tables,’ in columnar databases we have column families, which are containers for rows. Unlike relational databases, we don’t need to know all the columns up front and each row doesn’t have to have the same number of columns. Columnar databases are best suited for analyzing large datasets - big names include **Cassandra** and **HBase**.
* Graph Databases: These databases are used to store data whose relations are best represented in a graph. 

### High level differences between SQL and NoSQL
#### Storage
SQL stores data in tables where each row represents an entity and each column represents a data point about that entity; for example, if we are storing a car entity in a table, different columns could be ‘Color’, ‘Make’, ‘Model’, and so on.

NoSQL databases have different data storage models. The main ones are key-value, document, graph, and columnar. We will discuss differences between these databases below.
#### Schema
 In SQL, each record conforms to a fixed schema, meaning the columns must be decided and chosen before data entry and each row must have data for each column. The schema can be altered later, but it involves modifying the whole database and going offline.

In NoSQL, schemas are dynamic. Columns can be added on the fly and each ‘row’ (or equivalent) doesn’t have to contain data for each ‘column.’

#### Scalability
In most common situations, SQL databases are vertically scalable, i.e., by increasing the horsepower (higher Memory, CPU, etc.) of the hardware。

On the other hand, NoSQL databases are horizontally scalable, meaning we can add more servers easily in our NoSQL database infrastructure to handle a lot of traffic. 

#### Reliability or ACID Compliancy 
The vast majority of relational databases are ACID compliant. So, when it comes to data reliability and safe guarantee of performing transactions, SQL databases are still the better bet.

Most of the NoSQL solutions sacrifice ACID compliance for performance and scalability.

### Reason to use SQL
1. We need to ensure ACID compliance. ACID compliance reduces anomalies and protects the integrity of your database by prescribing exactly how transactions interact with the database.
2. Your data is structured and unchanging. If your business is not experiencing **massive growth** that would require more servers and if you’re only working with data that is consistent,


*     Structured data
*     Strict schema
*     Relational data
*     Need for complex joins
*     Transactions
*     Clear patterns for scaling
*     More established: developers, community, code, tools, etc
*     Lookups by index are very fast

### Reason to use NOSQL
1. Storing large volumes of data that often have little to no structure
2. Rapid development. NoSQL is extremely useful for rapid development as it doesn’t need to be prepped ahead of time


* Semi-structured data
* Dynamic or flexible schema
* Non-relational data
* No need for complex joins
* Store many TB (or PB) of data
* Very data intensive workload
* Very high throughput for IOPS

#### Sample data well-suited for NoSQL:

* Rapid ingest of clickstream and log data
* Leaderboard or scoring data
* Temporary data, such as a shopping cart
* Frequently accessed ('hot') tables
* Metadata/lookup tables



## Consistent Hashing
### Why consistent Hashing
1. Normal hashing is NOT horizontally scalable when using in Distribute cache
2. Normal hashing is NOT load balanced, especially for non-uniformly distributed data

