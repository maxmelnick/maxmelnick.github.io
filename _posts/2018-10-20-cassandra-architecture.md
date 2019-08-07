---
layout: post
title: An Introduction to Apache Cassandra for Architects, Ops, and Developers
---

**tl/dr:** Apache Cassandra is a NoSQL database with flexible deployment options that’s highly performant (especially for writes), scalable, fault-tolerant, and proven in production. Common use-cases include IoT, messaging, and fraud detection. You probably shouldn't use Cassandra if you have a small dataset, have highly transactional data, or need to do joins/aggregations without other tools. Alternative NoSQL databases include Amazon DynamoDB, Apache HBase, and MongoDB.

{% include image.html width="956" height="640" src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Cassandra_logo.svg/2000px-Cassandra_logo.svg.png" %}

In this post, I'll introduce you to Apache Cassandra, a tool I've been using in Production over the last two years. I'll provide an overview of what Cassandra is, when you should use it, when you shouldn't use it, and some alternatives.

## What is Apache Cassandra?

Apache Cassandra is an open-source NoSQL database that incubated out of Facebook to deal with the complexities of managing massive amounts of data.

## When you should use Cassandra

Cassandra is great for storing data when you need...

* A tool that’s **proven in production.** Major tech companies use it in production at scale. Apple has a production cluster with 75,000 nodes that stores over 10 PB of data. Netflix has a cluster that is 2,500 nodes, and supports 420 TB of data and over 1 trillion requests per day. Cassandra also has a vibrant open-source community (Apache top-level project for 10+ years) and has commercial support available through third-parties such as DataStax.
* **High performance (especially writes) on massive datasets.**  Cassandra's leaderless distributed architecture allows it to support very fast writes and pretty-fast reads on massive datasets. Additionally, Cassandra's linear scalability allows it to scale to accommodate growing datasets without sacrificing performance.
* **Fault-tolerance.** Cassandra's data replication and leaderless architecture means you won’t experience any downtime or data loss if a node goes down. You can even deploy Cassandra to be able to withstand the loss of an entire data center or geographic region.
* **Flexible deployment options.** You can deploy Cassandra on-prem, in the cloud or even a hybrid of the two.

{% include image.html width="956" height="500" src="https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/Cassandra-History.png" caption="History of Apache Cassandra. Image source: https://data-flair.training/blogs/apache-cassandra-tutorial/" %}

Common Cassandra use-cases include...

* Storing time-series data (e.g., logs, IoT sensor data)
* Messaging applications
* Fraud detection

## When you should NOT use Cassandra

You probably shouldn’t use Cassandra if you...

* **Have highly transactional data.** Cassandra can be problematic when data is updated or deleted frequently (updates/deletes) and/or needs to be consistent (e.g., invoicing system).
* **Have a small dataset.** The steeper learning curve and additional technical/operational complexity than traditional RDBMSs isn’t worth it if you don’t need to support massive data sets.
* **Need to do joins or aggregations without another tool.** Cassandra doesn’t support joins or aggregations. Instead of joins, Cassandra is designed to store data denormalized according to how you need to read it. You can also use analytic tools such as Apache Spark to support joins and aggregations on Cassandra data.

## Cassandra alternatives

Alternatives NoSQL databases include...

* **AWS DynamoDB.** DynamoDB and Cassandra originated from the same paper: [Dynamo: Amazon’s Highly Available Key-value Store](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf). DynamoDB is fully-managed and easier to get started with, but is less flexible (e.g., no tunable replication factor) and can be more expensive under a lot of workloads. [This article](https://www.beyondthelines.net/databases/dynamodb-vs-cassandra/) provides a more detailed comparison of the two.
* **HBase.** HBase is more operationally complex to configure, secure, and maintain as it requires other tools (e.g., Zookeeper) to run. Cassandra excels at writes, whereas HBase is better at reads. Cassandra struggles with data consistency, while HBase struggles with data availability. However, both have mechanisms to mitigate those shortcomings. See [this article](https://www.scnsoft.com/blog/cassandra-vs-hbase) for more information.
* **MongoDB.** As summarized in [this article](https://www.theserverside.com/tip/A-side-by-side-comparison-of-MongoDB-and-Cassandra-databases), "If you want a database that's similar to MySQL and the like but offers somewhat more flexibility and scalability, choose Cassandra. If you need a higher degree of flexibility and are willing to learn some new tricks, MongoDB's your answer."

## Learn more about Cassandra

Interested in learning more? You should check out...

* [Official Apache Cassandra website](http://cassandra.apache.org/)
* [Cassandra Wikipedia page](https://en.wikipedia.org/wiki/Apache_Cassandra)
* [Cassandra Github Repository](https://github.com/apache/cassandra)
* [DB-Engines Cassandra profile](https://db-engines.com/en/system/Cassandra)
* [Cassandra Explained in 5 Minutes or Less](https://www.credera.com/blog/technology-insights/java/cassandra-explained-5-minutes-less/)
* [What is Cassandra good for?](https://www.datastax.com/dev/blog/what-cassandra-good)
* [The Untold Story of Apache Cassandra](https://www.datastax.com/wp-content/uploads/resources/whitepaper/DataStax-eBook-The_Untold_Story_of_Apache_Cassandra.pdf?)
* [Cassandra Use Cases: When To Use And When Not To Use Cassandra](https://blog.pythian.com/cassandra-use-cases/)
