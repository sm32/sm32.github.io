---
layout: inner
title: Micro-services for Data Science
date: 2016-05-12 12:00:00
categories: data science
tags: microservices java datascience data science
---

### eCommerce industry data is a mix of good data (relational) and unstructured data like web clickstream or ad campaigns.
This inherit split forces a data scientist to setup elaborate ETL's and cleaning jobs which in all probability ends up being a waste of precious resources.

Problems of this nature can't have a single solution and we at Staples are trying multiple frameworks to help achieve speed an efficiency. Micro-services is not new for software industry or for that matter data science, there are a lot of interesting ideas/implementations by some really good people and all of those follow the rule of being small, robust, self sustaining and fault tolerant systems.

How small of a system is small enough is kind of tricky and varies based on the what you plan to do with it. Eg - Let's assume we have a ftp service, should it monitor the FTP? or download the file? or may be it can do more or less, This is an important design consideration, probably "THE" most important consideration which will impact applications built on top of the service.

Our problem of managing structured, unstructured data together for modeling and ML problems lead to solutions used in software industries namely QUEUES (Kafka/Rabbitmq). Queues have very interesting properties, they are fault tolerant, have easier disastror 
