---
Created: 2023-07-24 15:13
aliases:
  - sns
card link:
  - "[[Amazon Web Services]]"
---

## Description
---

Simple Notification Service is a pub-sub messaging service that sends information between applications, allowing message communication. e.g While deploying a product to SAAS on AWS, AWS recommends this service to publish customer sub/un-sub/buying information.

### Setting Up

There are only two things to setup SNS service.

1. [[Identity And Access Management (IAM)]]
2. Topics

Topics like tags to identify the type of messages. Other applications, i.e [[Simple Queue Service (SQS)]] , could distinguish which kind of message to receive.

In order to bind with other services, i.e [[Simple Queue Service (SQS)]], we need ARN(Amazon Resource Name). Using SQS as an example.

First, we need the ARN of the target queue.  
![[截圖 2023-07-24 下午4.22.55.png]]

Second, setup permissions for SNS to send message to SQS. Using IAM  
![[截圖 2023-07-24 下午4.25.08.png]]

Third, subscribe queue to SNS topic.  
![[截圖 2023-07-24 下午4.25.49.png]]

Forth, give the application or users appropriate permission to access the queue.![[截圖 2023-07-24 下午4.26.36.png]]  
![[截圖 2023-07-24 下午4.26.44.png]]