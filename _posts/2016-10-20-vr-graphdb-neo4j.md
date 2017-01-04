---
layout: inner
title: Visitor recognition using Graph Database (Neo4j)
date: 2016-10-20 12:00:00
categories: data science
tags: neo4j java datascience data science cookie visitor recognition
use_math: true
---

### Visitor recognition - An inference approach to consolidate multiple identifiers and improve recognition.
How can we say a given cookie X is the same as previously visited 10 other cookies? Can we data science help?
Organizations have become highly efficient in tagging an cookie with PII and most of it lost as soon as the user clears his/her cookies. With most websites having high ratio of return customers (> ~40% then new customers), it would be nice to understand who is visiting, how to better user experience with the side and customize offers.

Customers in their bid to remain "anonymous/new" try everything from incognito to deleting cookies. There are some serious research papers written on how companies subvert these attempts ([One such attempt](https://panopticlick.eff.org)), said that, these approaches are engineering solutions rather a data science. Most would rather try a quick solution owing to resource constrains.

Our motivation was to understand if data science can improve over existing methods and can it be done at scale for extended durations, not so surprisingly the answer is yes for both.

#### Customer Attributes
A single identifier (like email) doesn’t tell who the customer (eg - it could a person using someone else's machine for few mins), it's measly information. Thankfully tagging solutions pitch in with huge amounts of questionable meta-data about the user (questionable - because nothing about web clickstream is accurate) like the plugins, fonts, browsers, ip's etc, over a period of time it builds a customer profile.

### Graph Database
Thinking more, the problem itself is a graph problem, how can i find connected sub-graphs (cookies connected to cookies via meta data)? and so is the data! So obviously I wanted to plug the data into a graph DB, we chose [Neo4j](https://neo4j.com/) ([Giraph](http://giraph.apache.org/) was an equal contender).

#### Data data data
Anyone who has dealt with clickstream (adobe) data, knows the pain of missing/corrupt data, and if I start writing the cleaning process it will be a blog in itself (Kindly excuse this happy exclusion). The important part though to know is to transform data which suits Neo4j needs.

Each row is a record of a cookie with all the identified/meta data for a given **session**.

|Cookie Id   | Other Identifiers | Meta Data |
|:----------:|:-----------------:|:---------:|
|CI_001      | email, phone      | zip       |

Neo4j makes importing nodes (cookie_id) and making relationships (with identifiers) real easy (no-brainer steps), I created individual list's of identifiers (cookie/email/phone) and built relationships using the above table (simple enough!). Refer to the code base (**pending**) for more information on how to's.

With easy part over, I wanted to check if graph connections were correct. A quick check and I got this.

![Image description](/images/graph_example_connection.png)

Looks about right, the next step in the process is to identify sub graphs. Sub graphs in neo4j - turns out is not as simple as said and done. This needs java intervention, neo4j doesn't support complete graph scan, there is not syntax in Cypher (at least at the time of this project) which would support calculating sub graphs by scanning the complete graph. [Repo](https://github.com/SreekanthMahesala/neo-plugins) for plugins.

The recognition rate calculated using
 $$UNIQUE COOKIES HAVING IDENTIFIER/TOTAL UNIQUE COOKIES$$
increased by 10%, which was unheard of using traditional methods!

### Summary
Using graph DB's and some heavy lifting on data transformation, we were able to "de"anonymize traffic, found there are certain limitation to graph DBs, however, advantages outweigh problems and a fancy engineering solution may be an overkill. I am personally excited to work with graph DB's knowing it's potential!
