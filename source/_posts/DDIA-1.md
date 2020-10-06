---
title: DDIA_1
date: 2020-10-05 22:21:16
categories:
tags: DDIA
---
# Chapter 1 - Reliable, Scalable and Maintainable Applications

## Reliability
making systems work correctly, even when faults occur. 



Expetaction for reliable software

* The application performs the function that the user expected.
* It can **tolerate the user making mistakes or using the software in unexpected ways**.
* Its performance is good enough for the required use case, under the expected load and data volume.
* The system **prevents any unauthorized access and abuse**.

##### Fault vs Failure
Fault - a component of the system deviating from spec 

Failure - the system as a whole stops providing the required service to the user

You should generally prefer tolerating faults over preventing faults.

#### Hardware faults
Until recently redundancy of hardware components was sufficient for most applications

#### Software errors
#### Human erros

## Scalability
Scalability is the term we use to describe a system’s ability to cope with increased load.

#### Describing load
we need to succinctly describe the current load on the system; only then can we discuss growth questions

* a web server QPS
* ratio of reads to writes in a database,
* he number of simultaneously active users
* cache hit rate

#### Describing performance

what happens when the load increases:

1. When you increase a load parameter and keep the system resources (CPU, mem‐ ory, network bandwidth, etc.) unchanged, how is the performance of your system affected?
2. When you increase a load parameter, how much do you need to increase the resources if you want to keep performance unchanged?


* Batch processing systems like Hadoop care about throughput, number of records we can process per second.

* Online systems care about response time, the time between sending a request and receiving a response. Response time will vary with identical calls, so should be thought of as a distribution of values, not a single number.
 
* Percentiles are usually the best way to describe this distribution: p50, p95, p99, p99.9.

#### Approaches fro coping the load

* Scaling up or vertical scaling: Moving to a more powerful machine
* Scaling out or horizontal scaling: Distributing the load across multiple smaller machines.
* Elastic systems: Automatically add computing resources when detected load increase. Quite useful if load is unpredictable.

## Maintainability
* Operability - Make it easy for operations teams to keep the system running smoothly.
* Simplicity - Make it easy for new engineers to understand the system, by removing as much complexity as possible from the system. (Note this is not the same as simplicity of the user interface.)
* Evolvability- Make it easy for engineers to make changes to the system in the future, adapting it for unanticipated use cases as requirements change. Also known as extensibil‐ ity, modifiability, or plasticity

