---
layout: inner
title: Micro-services for Data Science
date: 2016-09-20 12:00:00
categories: datascience
tags: microservices java datascience data science
---

### eCommerce industry data is a mix of good data (relational) and unstructured data like web clickstream or ad campaigns.
This inherit duality of data forces a data scientist to setup elaborate ETL's and cleaning jobs which in all probability ends up being excessive.

We at Staples are trying multiple frameworks to help achieve speed an efficiency and in our endeavor found Micro-services to be a very good (if not perfect) solution. Micro-services is not new for software industry or for that matter data science, there are a lot of interesting ideas/implementations by some really good people and all of those follow the rule of being small, robust, self sustaining and fault tolerant systems. How small of a system is small enough is kind of tricky and varies based on the what you plan to do with it. Eg - Let's assume we have a ftp service, should it monitor the FTP? or download the file? or may be it can do more or less, This is an important design consideration, probably "THE" most important consideration which will impact applications built on top of the service.

At staples we choose small enough with a pinch of salt, some systems do a single task and others - many, with one commonality - they all use Queue's extensively.

### Implementation - Rabbitmq

Our implementation is simple yet highly flexible, each of the process boxes below are a group of processes, all listening to different sources and pushing data to queue. The queue/exchange ([Rabbitmq Exchanges](https://www.rabbitmq.com/tutorials/tutorial-three-java.html) are very powerful) decides next steps based on source, data and exchange/queue itself.

![Image microservices architecture](/images/microservices_architecture.svg)

There is one layer missing, what happens after R/Python execution? We plugin the outputs to databases, files, json's and even API calls, it's assumed given hence not represented. Also, feedback loop is missing (it's a bit more complicated and I didn't want to go into weeds of it - you would see lines flying all over this diagram!)
