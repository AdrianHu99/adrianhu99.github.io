---
title: July 1st half notes
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-17 15:49:43
summary:
tags: [Sharing, Architecture]
categories: [Tech]
password:
---

## Integration styles
<!--more-->
### 1. [File Transfer](https://www.youtube.com/watch?v=_uRYlUuxjVA&list=PLdsOZAx8I5umhnn5LLTNJbFgwA3xbycar&index=66)

FTP, HDFS, SCP, SMB, CIFS

**Pros:**

1. Universal integration style
2. Integration simplicity
3. System abstraction

**Cons:**

1. Error processing
2. Data synchronization timeliness
3. Data-only transfer

### 2. [Shared Database](https://www.youtube.com/watch?v=CSAFJNoT34M&list=PLdsOZAx8I5umhnn5LLTNJbFgwA3xbycar&index=65)

SQL, ODBC, JDBC, OLE-DB, RDA

**Pros:**

1. Near-universal integration
2. System abstraction
3. System decoupling
4. East of integration

**Cons:**

1. Doesn't work well with ORM (A can't assume table is not touched by others)
2. performance bottleneck issues (if too many apps attached to the same db)
3. Schema change issues
4. Data ownership issues

### 3. [Remote Procedure Call](https://www.youtube.com/watch?v=OGgbajZNwpU&list=PLdsOZAx8I5umhnn5LLTNJbFgwA3xbycar&index=64)

REST, SOAP, RMI (Remote Method Invocation), CORBA (Common Object Request Broker Architecture), WebSockets , CGI (Common Gateway Interface)

**Pros:**

1. preserve data encapsulation and ownership
2. external systems integration
3. mature frameworks and tools

**Cons:**

1. tight system coupling (if B is down, A has no other ways to defer it)
2. async communication (on truly queueing mechanism with RPI)
3. broadcast capabilities

### 4. [Messaging](https://www.youtube.com/watch?v=Oq5VP0cKwXI&list=PLdsOZAx8I5umhnn5LLTNJbFgwA3xbycar&index=63)

JMS (Java Message Service), MSMQ (Microsoft Message Queue), AMQP (Advanced Message Queuing Protocol), AWS SNS, AWS SQS, STOMP (Simple Text Oriented Messaging Protocol), SMPP (Short Message Peer-to-Peer SMS Messaging), MQTT (MQ Telemetry Transport - M2M/IOT Messaging), JT/400 (AS400 Data Queue)

**Pros:**

1. Highly decoupled system
2. Guaranteed delivery
3. Async communication
4. Broadcast capabilities
5. East of scalability

**Cons:**

1. Integration beyond firewall (RPI shines here)
2. Implementation complexity
3. Testing complexity
4. Cross platform standards
5. Async error handling

## The Good Parts of AWS with Daniel Vassallo

[link](https://softwareengineeringdaily.com/2020/07/07/the-good-parts-of-aws-with-daniel-vassallo/)

They talked about AWS technologies, with the focus on what you really need to build an application. Some notes I have: 

1. You might be disappointed with DynamoDB if you get from RDBMB to that. It's more similar to Redis than MySQL;
2. Always use EC2 by default;
3. With S3 you can separate storage and computing, one of the least appreciated values of S3 is you can think of S3 as having infinite bandwidth for all practical purposes. And use the default one at the beginning.
4. Default to network load balancers in general as ALB has some scale issues but NLB generally won't because it's a big multi-tenant router, you will have to use all of AWS's capacity to have issues.

