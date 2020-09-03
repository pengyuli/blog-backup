---
title: 'Long polling, WebSockets, and Server-Sent Events'
date: 2020-09-02 23:38:57
tags: System Design
---

Building a real-time web application is a bit challenging one, where we need to consider how we are going to send our data from the server to the client. There two general approaches: client pull or server push.

* Long/short polling (client pull)
* WebSockets (server push)
* Server-Sent Events (server push)


## Polling:
### Ajax Polling
In Ajax polling, a client makes XHR(XMLHttpRequest)/Ajax requests to server repeatedly at some regular interval to check for new data.

A flow for Ajax polling will as follow.

* A client initiates requests at a small regular intervals (e.g 0.5 Seconds)
* The server prepares the response and sends it back to to the client just like normal HTTP requests.

### Long Polling
Long polling is technique where the server elects to hold a client connection open for as long as possible, delivering a response only after data becomes available or timeout threshold has been reached. After receiving response client immediately sends the next request.

### Issue of using polling
##### Header Overhead:
With the HTTP long polling technique, every long
poll request and long poll response is a complete HTTP message and
thus contains a full set of HTTP headers in the message framing.
For small, infrequent messages, the headers can represent a large
percentage of the data transmitted.  If the network MTU (Maximum
Transmission Unit) allows all the information (including the HTTP
header) to fit within a single IP packet, this typically does not
represent a significant increase in the burden for networking
entities.  On the other hand, the amount of transferred data can
be significantly larger than the real payload carried by HTTP, and
this can have a significant impact (e.g., when volume-based
charging is in place).

##### Maximal Latency:  
After a long poll response is sent to a client, the
server needs to wait for the next long poll request before another
message can be sent to the client.  This means that while the
average latency of long polling is close to one network transit,
the maximal latency is over three network transits (long poll
response, next long poll request, long poll response).  However,
because HTTP is carried over TCP/IP, packet loss and
retransmission can occur; therefore, maximal latency for any
TCP/IP protocol will be more than three network transits 

##### Reliable message ordering 
can be an issue with long polling because it is possible for multiple HTTP requests from the same client to be in flight simultaneously.

## Websockets
It provides a persistent connection between a client and a server that both parties can use to start sending data at any time. 
WebSockets keeps the connection open, allowing messages to be passed back and forth between the client and the server. In this way, a two-way ongoing conversation can take place between the client and the server.

### Pros
* WebSockets keeps a unique connection open while eliminating latency problems that arise with Long Polling.
* WebSockets generally do not use XMLHttpRequest, and as such, headers are not sent every-time we need to get more information from the server. This, in turn, reduces the expensive data loads being sent to the server.

### Cons
WebSockets don’t automatically recover when connections are terminated – this is something you need to implement yourself


## Server Sent Events
Under SSEs the client establishes a persistent and long-term connection with the server. The server uses this connection to send data to a client. If the client wants to send data to the server, it would require the use of another technology/protocol to do so.Server-Sent Events are a one-way communication channel where events flow from server to client only. 