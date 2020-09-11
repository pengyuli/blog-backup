---
title: network_nots
date: 2020-09-11 00:01:37
categories: network
tags: network
---

## 5 Layer Model
![Imgur](/images/Computer_Networking/5layer.png)
![Imgur](/images/Computer_Networking/Encapsulation.png)

#### 4 layer model: 
doesn’t differentiate between the physical layer and the data link layer

#### OSI Model
OSI model abstracts the application layer into three layers total.

### Example of relation betwen layers
![Imgur](/images/Computer_Networking/5layer_example.png)

The physical layer is the delivery truck and the roads.
The data link layer is how the delivery trucks
get from one intersection to the next over and over.
The network layer identifies which roads need
to be taken to get from address A to address B.
The transport layer ensures that delivery driver knows
how to knock on your door to tell you your package has arrived.
And the application layer is the contents of the package itself. 

## Physical Layer

## Data link Layer	
the data link layer is responsible for
defining a common way of interpreting these signals,
so network devices can communicate. 

#### MAC Address
a globally unique identifier attached to an individual network interface. 

First three octes of Mac Address: Organizationally Unique Identifier(OUI)

#### Unicast, Multicast, and Broadcast
##### Unicast
A unicast transmission is always meant for just one receiving address.

At the Ethernet level,
this is done by looking at a special bit in the destination MAC address.
If the least significant bit in the first octet of a destination address is set
to zero, it means that Ethernet frame is intended for only the destination address.
This means it would be sent to all devices on the collision domain, but
only actually received and processed by the intended destination. 

#### Multicast
A multicast frame is similarly set to all devices on the local network signal.
What's different is that it will be accepted or discarded by each device
depending on criteria aside from their own hardware MAC address. 

#### Broadcast
An Ethernet broadcast is sent to every single device on a LAN.
This is accomplished by using a special destination known as a broadcast address

## Network Layer
allows different networks to
communicate with each other through devices known as routers.

**delivering datagram to computers -- ip address**

#### Protocol in this layer: IP
![Imgur](/images/Computer_Networking/IPHeader.png)

#### Address Resolution Protocal ARP
ARP is a protocol used to discover the hardware address of a node with a certain
IP address. 
## Transport Layer
the transport layer sorts out which client and server programs are supposed to get that data.

**delivering data to applications -- port number**

#### Protocol in this layer: TCP UDP
##### Multiplexing & demultiplexing
Multiplexing in the transport layer means that nodes on the network have the ability
to direct traffic toward many different receiving services.
Demultiplexing is the same concept, just at the receiving end,
it's taking traffic that's all aimed at the same node and
delivering it to the proper receiving service. 
##### Port
The transport layer handles multiplexing and demultiplexing through ports.
A port is a 16-bit number
that's used to direct traffic to specific services running on a networked computer. HTTP 80 is for HTTP web traffic. FTP in port 21

IP + Port: 10.1.1.100:80 --> Socket numberor socket address

## Application Layer

#### Protocol in this layer: HTTP SMTP
