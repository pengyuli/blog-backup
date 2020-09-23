---
title: Databases
date: 2020-09-15 21:03:29
categories: AWS
tags: AWS
---

# Databases

## AWS DB
RDS:

* SQL
* MySQL
* PostgreSQL
* Oracle
* Aurora
* MariaDB

DyanmoDB - No SQL

RedShift - OLAP

Elasticache - In Memeory Caching

## RDS 
* **RDS runs on virtual machines**, **not serverless** (Aurora is exception)
* User cannot login to these operation systems
* 

### Automated Backups
There are two different types of backups for AWS:

1. Automated: Are enabled by default, data is stored in S3 and are enable automatically. If you delete the DB, the backup will de belated too
2. Database snapshots: Need to be done manually, they are kept even if you remove the DB.

When you restore a backup or a snapshot, the restored version of the database will be in a new RDS instance, with a new DNS name

### Encryption 
You can encrypt your Amazon RDS DB instances and snapshots at rest by enabling the encryption option on your Amazon RDS DB instances. 

### RDS Multi-AZ

When you provision a Multi-AZ DB Instance, Amazon RDS automatically creates a primary DB Instance and synchronously replicates the data to a standby instance in a different Availability Zone.
If DB instance failure or avaliability zone failure, Amazon RDS will automatically failover to the standby so db operation can resume

it's for disaster recovery not for scaling.

### RDS Read Replicas

* This feature makes it easy to elastically scale out beyond the capacity constraints of a single DB Instance for read-heavy database workloads The read replica operates as a DB instance that allows only read-only connections
*
* It's used for scaling not for disaster recovery
* You need to have automatic backups on in order to have a read replica.
* You can have up to 5 read replicas of any DB at the time of writing.
* Each replica has its own DNS name.
* Replicas can become their own databases.
* You can have a replica in a second region.
* You can enable encryption on your replica even if your master is not.
* Available for MySQL, PostgreSQL, Oracle, Aurora, MariaDB


## DynamoDB
* Uses SSD storage.
* Spread across 3 distinct data centres.
* Eventual Consistent Reads (Default)
* Strongly Consistent Reads(result reflects all writes that receivd a successful response)
* It's scalable.
* DynamoDB can be very expensive for writes.


### DAX DynamoDB Accelerator


## Redshift

Amazon Redshift is a fast, scalable **data warehouse** that makes it simple and cost-effective to analyze all your data across your data warehouse. **Only avaliable in one AZ**

Redshift stores data by colums. By storing data in columns rather than rows, the database can more precisely access the data it needs to answer a query rather than scanning and discarding unwanted data in rows. Query performance is increased for certain workloads.

Columnar data stores can be compressed much more than row-based data.



* Single node: You can start with a single node (Up to 160Gb of ram in one node)

* Multi-Node:

    * Leader node: Manages clients and distribute queries
    * Compute nodes: Store data and execute queries (up to 128 computer nodes max)

### Back up
* Enabled by default with a 1 day retention period
* Maximum retention period is 35 days
* Always attempts to maintain at least 3 copies of your data.(original and replica on the compute nodes and a backup in S3)
* Redshift can asynchronously replicate snapshots to S3 in another region for disaster recovery

## Aurora

* 2 copies of your data are contained in each availability zone with minimum of 3 avaliability zone. 6 copies of data

* Aurora snapshot can share with other AWS accounts
* 3 typs of relicas avaliable, Aurora, MySQL and PostgresQL
* Aurora has automated backups turned on by default.
* Aurora serverless
    * Aurora serverless provides a relatively simple and cost effective option for infrequent, intermittent or unpredictable workloads


## Elasticache
Types of Elasticache:

* Memcached
* Redis: In memory key-value store

## DMS data base migration service
* Allow migrate db from one source to SWS
* you can do homogenous migration(Same DB) or heterogenous(Different DB) migration
* Source can be on premises, or inside SWS or another cloud provider such as Azure
* AWS SCT(schema conversion tool) for heterogenous migration
   



