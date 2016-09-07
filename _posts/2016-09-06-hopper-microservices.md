---
layout: inner
title: Microservices and data science
date: 2016-05-12 12:00:00
categories: data science
tags: microservices java datascience data science
---

### After dealing with systems which broke at the slightest sign of change.
We had to think radically about what systems design mean in the context of data science.
The obvious things like moving to nosql data stores was done, however, monolithic design lead to failures which were almost always major bugs.
In comes "QUEUES", an elegant way to break up a huge system into smaller subsystems which can be generic/reliable and fault tolerant.

Microservices is not new, however writing up with the help of queues made my life so much more fun!
I now have services, each one talking to a specific exchange/queue based on the algorithm requirements, execute and push the results back to queue for further processing.

