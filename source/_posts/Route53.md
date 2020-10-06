---
title: Route53
date: 2020-09-24 23:00:47
categories: AWS
tags: AWS
---
# Route53

### Domin Name
* you can by domain name from AWS
* It can take up to 3 days to register domain name

## Routing

### Simple Routing Policy
You can only have 1 record with multiple addresses.If specify multiple values in a record, Route 53 returns all values to user in random order
### Weighted Routing Policy
Allow you split your traffic based on different weight you set
### Latency Routing Policy 
Allows you to route traffic based on the lowest network latency for end user
### Failover Routing Policy
Use when you want to configure active-passive failover. You need to create a health check before.
### Geolocation Routing Policy
Use when you want to route traffic based on the location of your users.
### Geoproximity Routing(only in Route53 traffic flow)
route traffic to your resources based on geographic location of your users and your resources. You can slop optionally choose to route more/less to given resource by specifying a value(bias)
### Multivalue Answer Policy
simple routing + health check