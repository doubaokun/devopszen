---
layout: post
published: true
title: AWS RDS or self-managed MySQL
imagefeature: blog/mysql-vs-rds.png
mathjax: false
featured: true
comments: false
description: Should I choose self managed MySQL or AWS RDS (MySQL)
categories: 
  - database
tags: devops database aws rds mysql
---

Technical stack design and chosen is very important for initial stage start-ups. If we can do it right, the future issues could be avoided. There are many factors to build a scalable, cost efficient, high-performance system, but we will discuss a lot bit of the database vendor choices.

<p style="text-align: center;"><img src="https://www.devopszen.com/images/blog/mysql-vs-rds.png" alt="AWS RDS vs MySQL"/></p>

### MySQL vs MongoDB

MySQL is the most widely used database which supports ACID:

* Atomicity
* Consistency
* Isolation
* Durability

Compare with MongoDB (NoSQL), MySQL (RDBMS) can be used in the transactional system. Lots of e-commerce systems use MySQL as the core trading database. It is free, mature, with a big technical community.

### Features of AWS RDS

AWS RDS is a mantainance free MySQL system, you don't have to do:

* Hardware provisioning
* Database setup
* Software patching
* Data backup
* Setup and managed the read replica
* Manually setup if you like to switch to a larger instance

It provides the features such as:

* Hot standby at another available zone (Multiple AZ) and automatic switch over when the master database fails with in 2 minutes downtime
* Automatic backup and snapshot
* Automatic scale up or down (with downtime)
* Tunned High-performance network and I/O 

### Self-managed MySQL or AWS RDS

Compare the price of the RDS with the same CPU/disk EC2 instance (db.m4.large vs m4.large):

Aspect          | m4.large (EC2)| db.m4.large (RDS)| Multi-az RDS    |
--------------- | ------------- | ---------------- | --------------- |
Memory          | 8 GB          | 8 GB             | 8 GB            |
CPU             | 2 vCPUs       | 2 vCPUs          | 2 vCPUs         |
Storage         | -             | -                | -               |
Price           | $84.680       | $148.190         | $296.380        |

You can see the on-demand price of RDS is roughly double the price of self-managed MySQL on the similar EC2 instance; the price of multi-az RDS doubles the single instance RDS.

### How to choose

* If the database is running for critical business, you can choose multi-AZ RDS;
* If you have inhouse expert DBA, and system expert you can choose self-managed MySQL on EC2 instance;
* For average usage, We would recommend single instance AWS RDS.
