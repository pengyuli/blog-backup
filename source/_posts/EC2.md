---
title: EC2
date: 2020-09-23 22:00:51
categories: AWS
tags: AWS
---

# EC2
Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers.

## EC2 Options

### On Demand 
You pay for computing capacity by per hour or per second 
###Reserved

Provide a significant discount (up to 75%) compared to On-Demand pricing and provide a capacity reservation when used in a specific Availability Zone. You have to enter a contract.
### Spot
Amazon EC2 Spot instances allow you to request spare Amazon EC2 computing capacity for up to 90% off the On-Demand price.
###### Use case
* Big data and analytics
* Containerized workloads
* CI/CD and testing
* web service
* image and media rendering
* High performance computing

###### Not Good fit
* Persistent workloads
* Critical jobs 
* Databases

#### Spot fleet
a collection of spot instance and on demand instance
### Dedicated Hosts
Is a physical server with EC2 instance capacity fully dedicated to your use.

## Security Group
* All Inbound traffic is Blocked by Default.
* All outbound traffic is allowed
* Change to security group take effect immediately
* You can have many EC2 with in one Security group or many groups in one EC2
* Security Group is **STATEFUL**. For example, if you allow the request to come in, automatically responses can go out even if you don't have anything on the outbound section of your security group.
* You can specify only allow rules, not deny rules


## EBS volumes
Provides persistent block storage volumes for use with Amazon EC2 instances in the AWS Cloud. EBS is automatically replicated in a specific AZ




#### Types of EBS
![Protocol flow](/images/AWS/EBS.png)

* SSD are good for random access.
* HDD (Magnetic) Are great for sequential access (processing log files, bigdata work flows as an example).

## Volumes & Snapshots
* Volumes exist on EBS
* Snapshots exist on S3(Snapshots are point in time copies of Volumes)
* Snapshots are incremental-- This means only the clocks that have changed since your last snapshot are moved to S3
* First Snapshot will take some time to create

#### Move EC2 volume from one AZ to anotherr
Take a snapshot and create AMI from snapshot and then use the AMI to launch the EC2 instance in new AZ

#### Move EC2 colume to new Region
Take a snapshot and create AMI from snapshot and then copy AMI from one region to another, use the AMI to launch the EC2 instance in new region


## Amazon Machine Images (AMI) Types
An Amazon Machine Image (AMI) provides the information required to launch an instance. 

#### EBS
* EBS can be stopped, data will not lost if instance stopped

#### Instance Store
* Called Ephemeral storage sometimes, if stop instance store volumes, dat will be lost. Reboot is OK


## ENI vs ENA vs EFA

#### ENI
Elatic Network Interface - a virtual network card

##### Use case
Basic networking. Pherhaps you need a separate management network to your prod network or a separate logging networking and you need to do this at low cost

#### EN
Enhanced Networking. Uses single root I/O virtualization to provide high-performance networking capabilities on supported instance types

##### Use case
When you need speed between 10Gbps---100Gbps. 

#### EFA 
Elastic Fabric Adapter. A network device you can attach to your Amazon EC2 instance to accelerate High Performance Computing and machine learning applications

##### Use case
HPC(High Performance Computing) and machine learning applications


### Encrypted Root Device Volumes & Snapshot

* Snapshots of encrypted volumes are encrypted automatically
* Volumes restored from an encrypted snapshot will be encrypted as well.
* You can share snapshots only if they are not encrypted, these snapshots can be made public.


## EV2 Hibernate
Withe EC2 Hibernate, the instance boots much faster. The OS does not need to reboot because the in-memery state(RAM) is preserved.

* Preserves the in-memory RAM on persistent storage(EBS)

#### Use case
Loing-running processes
Service that take time to initialize


# CloudWatch
* Cloudwatch is used for monitor performance
* CLoudWatch can monitor most of AWS as well as your application that runs on AWS
* CloudWatch with EC2 default monitor events every 5 min. you can have 1 min by turning on detailed monitoring
* You can create Cloudwatch alarms 
* CloudWatch is about performace and CloudTrail is about auditing

# IAM with EC2
* Roles avoid you to store credentials inside EC2 instances in order to communicate with other AWS services
* Roles can be assigned after an EC2 instance it has been provisioned
* Roles are universal, you can use them in any region.

## EFS Elastic file system
* Support the Network File system version 4 NFSv4
* only pay for storage you use
* can scale up to petabytes
* support concurrent NFS connections
* Data is stored across multiple AZ within a region

## Amazon FSX
Amazon FSX is build on windows server and it provides a fully managed native Microsoft windows file system so you can seaily move you windows applications that require file storage to AWS

## FSX Lustre
Design for fast processing of workloads like ML and HPC, video processing and EDA

## EFS VS FSX VS FSX for lustre

EFS: when you need distributed, highly resilient storage for **Linux instances** and **Linux based apps**

FSX: When you need storage for **Windows based apps** such as Sharepoint, Microsoft SQL Server

FSx for Lustre: WHen you need high performance high capacity storage(ML, HPC)

## EC2 placement groups

#### Clustered placement group
A frouping of instance in same availability Zone. 
##### Use case
Low Network Latency/ High throughput
#### Spread placement group
spreads instances across underlying hardware and can spread in multiple Availability Zones.
##### Use case
Invididual Critical EC2 instance
#### Partition placement group
spreads instances across logical partitions, ensuring that instances in one partition do not share underlying hardware with instances in other partitions.

##### Use case
Nyktiple EC2 instance HDFS, HBase and Cassandra

## HPC with AWS
### Data Transfer
* Snowball, snowmobile
* AWS DataSync to store in S3, EFS, FEX for windows
* Direct Connct

### Compute and Networking
* EC2 that are GPU or CPU optimized
* EC2 fleets
* cluster placement groups(same region, low latency)
* Enhanced Networking
* Elastic Network Adaper
* Elastic Fabric Adapters

### Storage
Instance-attache storage:
* EBS
* Instance Store

### Network storage
* S3
* EFS
* FSx for lustre

### Orchestration & Automation
* AWS Batch
* AWS ParallelCluster


## AWS WAF
web firewall that let you control access to you content



