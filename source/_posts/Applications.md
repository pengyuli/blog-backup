---
title: Applications
date: 2020-09-22 21:08:31
categories: AWS
tags: AWS
---

# SQS
Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to **decouple** and scale microservices, distributed systems, and serverless applications.

* It's basically a message queue service, like Kafka for example. You add items in the queue, and then someone will ask for these objects from the queue.
* Retention can go up to 14 days.
* Messages are 256KB in size
* It's a **pull base** system.
* Type of queues:
	*     Default: All queue are standard by default. They don't have an order. Ordering is best-effort, so they don't guarantee ordering on default queues.
	*     FIFO: (first in first out) These queues guarantee ordering.
* You can have duplicates if you don't manage very well your visibility timeouts.


# SWF Simple Work Flow Service

Amazon SWF (Simple Workflow Service) is an Amazon Web Services tool that helps developers coordinate, track and audit multi-step, multi-machine application jobs.

* Retention can go up to 1 year
* SWF presents a tsk-oriented API

# SNS
* Instantaneous, push based delivery
* Simple APIs and easy integration with APP
* Flexible message delivery over multiple transport protocols. It can notify through:
	
	* AWS Lambda functions
	* HTTP/S webhooks
	* mobile push
	* SMS
	* email


# Elastic Transcoer
Amazon Elastic Transcoder a is media transcoding service in cloud.

# API Gateway
* Amazon API Gateway is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale.
* You can enable cache
* Scaled automatically, low cost
* You can throttle requests to prevent attack
* Connect to CloudWatch to log all requests.
* ensure enable CORS on API gateway if using Javascript that uses multiple domains


# Kinesis
Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data

### Kinesis Streams
Kinesis streams: It consists of **shards**, where each **stream is saved and stored for 24h**, up to 7 days. You can have multiple shards on each stream. A consumer then read from the shards and process the data.
### Kinesis Firehose
It doesn't have shards, so data traverses the Firehose. Data has to be processed immediately with lambda or stored in S3 for example.It can stream data to Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk.
### Kinesis Analytics
It allows you to analyze the data on fly in Kinesis Firehose or streams.

# Web Identity Federation - Cognito
* Federation allows users to authernticate with a Web Identity Provider (Google, Facebook. Amazon)




