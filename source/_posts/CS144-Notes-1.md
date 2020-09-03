---
title: CS144 Notes-1
date: 2020-09-03 01:08:29
categories: Networking
tags: CS144 Networking
---

### 4 Layer Internet Model
#### 4 layer compare to OSI Model
![Imgur](/images/CS144/L4_OSI.png)

### 4 Layer
![Imgur](/images/CS144/4Layer.png)

#### Link Layer
Transfer packet.
The link layer is to carry the data over one link at a time.

Link Layer example: Wifi, 4G, Ethernet

#### Network Layer
Network layer packets are called **datagrams**

##### IP Internet Protoal
- IP attemp to deliver datagrams to the other end but no promises
- IP datagrams can get lost, deliver out of order and can be corrupted. No guarantees.

#### Transport Layer
##### TCP Transmission Control Protocol
- Transfer data gurantee delivery and in order

##### UPD User Datagram Protocol
- No gurantee but fast

#### Application Layer
Application layer protocol example: HTTP


[checksum](https://www.tutorialspoint.com/error-detecting-codes-checksums)


### IP
Why IP is so simple?

* To keep the network simple, dumb and minimal
* End-to-end principle: implement the features in the end hosts
* Allows a variety of reliable (or unreliable) services to be built on top
* requires very few assumptions of the link layer below


