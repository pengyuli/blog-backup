---
title: OSI-Application Layer
date: 2020-09-03 01:10:09
categories: Networking
tags: TCP UPD ApplicationLayer
---
![OSI](/images/OSI.png)

# Application Layer
## Hypertext transfer protocol (HTTP)
HTTP is a method for encoding and transporting data between a client and a server. It is a request/response protocol: clients issue requests and servers issue responses with relevant content and completion status info about the request. HTTP is self-contained, allowing requests and responses to flow through many intermediate routers and servers that perform load balancing, caching, encryption, and compression.

HTTP is an application layer protocol relying on lower-level protocols such as **TCP** and **UDP**.
## Tranportation Layer
### TCP Transmission control protocol 
TCP is a **connection-oriented** protocol over an IP network. All packets sent are **guaranteed to reach the destination in the original order and without corruption** through:

* Sequence numbers and checksum fields for each packet
* Acknowledgement packets and automatic retransmission

If the sender does not receive a correct response, it will resend the packets. If there are multiple timeouts, the connection is dropped. TCP also implements flow control and congestion control. These guarantees cause delays and generally result in less efficient transmission than UDP.

TCP is useful for applications that **require high reliability but are less time critical**

### UDP User datagram protocol

UDP is connectionless. Datagrams (analogous to packets) are guaranteed only at the datagram level. Datagrams might reach their destination out of order or not at all. UDP does not support congestion control. Without the guarantees that TCP support, UDP is generally more efficient.

Use UDP over TCP when:

* You need the lowest latency
* Late data is worse than loss of data
* You want to implement your own error correction


