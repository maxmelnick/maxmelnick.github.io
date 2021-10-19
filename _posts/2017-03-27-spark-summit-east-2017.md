---
layout: post
title: Key Apache Spark Trends from Spark Summit East 2017
---

I was lucky enough to attend [Spark Summit East 2017](https://spark-summit.org/east-2017/) February 8-9. I had to brave the 12" of snow blizzard Nico brought to Boston, but overall learned a lot about the strategic direction of the [Apache Spark](http://spark.apache.org/) open source project and ecosystem. In this post I'll fill you in on the key Spark trends from the conference. This post will be helpful if you are part of an organization that is currently using Spark, looking to use Spark, or you are just personally interested in Spark.

<!-- {% include image.html width="700" height="170" src="assets/images/spark-summit-2017/spark-summit-banner.png" %} -->


{% include image.html src="https://pbs.twimg.com/media/C5DOQJpW8AIwACy.jpg" caption="Boston: Spark Summit East 2017 host city. Image source: https://pbs.twimg.com/media/C5DOQJpW8AIwACy.jpg" %}

>Disclaimer: The opinions expressed in this article are my own and do not reflect the view of any other individuals or organizations.


<!-- # Wait a second! What exactly is Spark, Spark Summit, and why should I care?

## Why Spark?
- Faster than previous generation distributed computing analytics tools such as Map Reduce. Spark achieves better performance by doing everything in-memory and separating compute and storage.
- Easier to develop than tools like Map Reduce. Spark is available in more
- Enabled analytics architecture consolidation with it's unified architecture for analytics means you can consolidate many existing

- https://www.mapr.com/blog/5-minute-guide-understanding-significance-apache-spark -->

# _Spark moves to Primetime:_ Key Spark Trends from Spark Summit East 2017

The overarching theme I took away from the conference was: _Spark moves to Primetime_. In other words, Spark is maturing from a tool used by "early adopter" analytics shops (small startups or corporations with mature analytics departments that use it mostly for development or offline analytics) to "early majority" analytics shops (large data-driven organizations that require tools be enterprise/production-ready). For those of you familiar with Geoffrey Moore's [book](https://www.amazon.com/Crossing-Chasm-Marketing-High-Tech-Mainstream/dp/0060517123), _Crossing the Chasm_, this is the "Chasm" for Spark adoption.

{% include image.html src="http://i1.wp.com/www.theinnovativemanager.com/wp-content/uploads/2014/10/Product-life-cycle-crossing-the-chasm.jpg" caption="Spark adoption reaches THE CHASM. Image source: http://i1.wp.com/www.theinnovativemanager.com/wp-content/uploads/2014/10/Product-life-cycle-crossing-the-chasm.jpg" %}


The _Spark in Primetime_ theme was clear in the conference's significant focus on Enterprise/Production-ready Spark. There was much discussion about making Spark more real-time focused, secure, and easier to operate (e.g., easier for IT to deploy and manage; easier for data scientists to access). The whole second day of the conference was even themed _Enterprise Day_!

<!-- In my mind, this Spark _move to Primetime_ is like the Apple iPhone boom circa 2010. Back then, there was a lot of buzz and demand for the iPhone, but AT&T was the only iPhone carrier and barely anyone had an iPhone for their work phone. In 2011 the iPhone experienced it's _move to Primetime_ when additional carriers picked it up (e.g., Verizon and Sprint). Many large organizations also started allowing their employees to connect iPhones to their work email. Now the iPhone is the standard in many organizations. Will Spark follow a similar path?? -->

The Spark community made a lot of these enterprise/production-ready features available in the recently released Spark 2.0. The newly formed [Berkeley RISELab][rise], the successor to the Berkeley AMPLab, is looking to take them to the next level.

{% include image.html src="assets/images/spark-summit-2017/riselab-enabling-intelligent-realtime-decisions-keynote-by-ion-stoica-5-1024.jpg" caption="RISELab: Enabling Intelligent Real-Time Decisions keynote by Ion Stoica" %}

## Easier to Operationalize Spark

The learning-curve and sustainability of a tool are frequently big hurdles to adoption. There was a strong focus on how to make Spark easier to operate (e.g., deploy, access, and manage) in an effort to decrease the learning-curve and make it a more sustainable solution.

Matei Zaharia, creator of the Spark project, discussed in his [keynote]([matei]) how Spark helps "democratize access to data." In other words, data engineers / scientists have the luxury of choosing from several programming languages when they write Spark code, including the more recent addition of R. Additionally, the high-level Spark APIs (Spark SQL, DataFrames, ML Pipelines, PySpark, SparkR) make Spark development easier.

{% include image.html src="assets/images/spark-summit-2017/trends-for-big-data-and-apache-spark-in-2017-by-matei-zaharia-19-1024.jpg" caption="Developers have several languages to pick from to use Spark, including the most recent addition of R" %}

In addition to easier access to data, many vendors in the Spark ecosystem pitched ways to simplify Spark deployment and management. The main sponsor, [Databricks](https://databricks.com/), heavily pushed the capabilities of their Spark cloud platform. The conference goodie bag had several flyers marketing "Data Science Sandbox" and "Data Science as a Service" solutions. BlueData [presented](https://spark-summit.org/east-2017/events/lessons-learned-from-dockerizing-spark-workloads/) on running Spark in Docker containers. Openshift [discussed](https://spark-summit.org/east-2017/events/teaching-apache-spark-clusters-to-manage-their-workers-elastically/) their platform, built on Docker and Kubernetes, that enables a "fully elastic Spark application with little more than the click of a button." All this focus on making it easier to operationalize Spark will help drive overall Spark growth.

{% include image.html src="assets/images/spark-summit-2017/lessons-learned-from-dockerizing-spark-workloads-spark-summit-east-talk-by-tom-phelan-29-1024.jpg" caption="Lessons Learned from Dockerizing Spark Workloads: Spark Summit East talk by Tom Phelan" %}

## "Continuous Applications"

While there are countless tools available to address streaming, batch, or data serving analytics workloads, it is difficult to create apps that integrate all three workloads. With Spark 2.0 (specifically Spark Structured Streaming), Spark aims to provide a single API for what Databricks is coining "continuous apps" - apps that merge streaming and batch workloads.

{% include image.html src="assets/images/spark-summit-2017/trends-for-big-data-and-apache-spark-in-2017-by-matei-zaharia-23-1024.jpg" caption="Matei Zaharia discussed how continuous applications integrate streaming, batch, and data serving workloads" %}

Similarly, the Principal Product Manager for MemSQL, Steven Camina, [discussed](https://spark-summit.org/east-2017/events/building-the-ideal-stack-for-real-time-analytics/) the massive opportunity of converting existing batch processes to real-time.

{% include image.html src="assets/images/spark-summit-2017/memsql-real-time.JPG" caption="Building the Ideal Stack for Real-Time Analytics, presented by Steven Camiña (MemSQL)" %}

Going forward, the [Berkeley RISELab][rise] will have a heavy focus on enabling "continuous apps" given the group's "real-time" focus:

{% include image.html src="assets/images/spark-summit-2017/riselab-enabling-intelligent-realtime-decisions-keynote-by-ion-stoica-9-1024.jpg" caption="RISELab: Enabling Intelligent Real-Time Decisions keynote by Ion Stoica" %}


## Faster Big Data Analytics

Right now, a major performance issue with big data analytics is the compute bottleneck. While storage and network performance improved ~10x since 2010, CPU performance has remained relatively stagnant.

{% include image.html src="assets/images/spark-summit-2017/trends-for-big-data-and-apache-spark-in-2017-by-matei-zaharia-11-1024.jpg" caption="In his keynote, Matei Zaharia discussed the existing compute bottleneck created by the limited increase in CPU performance since 2010" %}

To address this issue, the Spark community created Project Tungsten with the goal of optimizing Spark CPU and memory usage.

{% include image.html src="assets/images/spark-summit-2017/trends-for-big-data-and-apache-spark-in-2017-by-matei-zaharia-16-1024.jpg" caption="Impact of Project Tungsten slide from Matei Zaharia keynote" %}


## Security

A big hurdle to Enterprise adoption and Production use is security. Spark security is about to get a big upgrade with the introduction of the Berkeley RISELab.

As I mentioned earlier, the goal of the [RISELab][rise] is to enable "Real-time decisions on live data with strong security." The RISELab has two projects to address the "strong security" component:

- *Secure Real-time Decisions Stack (SRDS):* open source platform to develop RISE apps, secure from the ground up
- *[Opaque:](https://www.slideshare.net/SparkSummit/opaque-a-data-analytics-platform-with-strong-security-spark-summit-east-talk-by-wenting-zheng)* secure distributed data analytics framework

{% include image.html src="assets/images/spark-summit-2017/riselab-enabling-intelligent-realtime-decisions-keynote-by-ion-stoica-18-1024.jpg" %}

{% include image.html src="assets/images/spark-summit-2017/opaque-a-data-analytics-platform-with-strong-security-spark-summit-east-talk-by-wenting-zheng-16-1024.jpg" caption="Opaque: A Data Analytics Platform with Strong Security. Talk by Wenting Zheng" %}



<!-- ## Standout Vendors (in my opinion)

Say something about the expo...

The typical big vendors (Cloudera and IBM),

Heavy on products and platforms vs services (probably because higher margins).

### Databricks

### MemSQL

I've heard a lot of great things about MemSQL, the [insert explanation here]. I was impressed by their presentations, their capability, and the types of clients they're working with (based off a conversation I had with the folks at their expo booth)

### Other notable vendors

Mesosphere
Redislabs
bluedata
STREAMANALYTIX

Check out [this page](https://spark-summit.org/east-2017/sponsors/) for a full list of conference sponsors/vendors.

# My Favorite Spark Summit 2017 Presentations

## My Favorite Presentations

## Other Presentations I Attended -->


# What's next?

As Spark makes the move to _Primetime_, crossing the chasm to the "early majority" of true enterprise adoption, will you take advantage of all that Spark can do for you?

To learn more about how Spark can help you, check out all the [presentation videos and slides from Spark Summit East 2017](https://spark-summit.org/east-2017/schedule/).

<!--- talk at (or go to) future Spark Summit
- The conference organizers do an amazing job of making the video and slides from each presentation available to everyone. Take a look at the full list of presentations and see if there's something you might like!
 - learn more about Spark (blogs, resources, etc.)
- Follow the RISELab
- Contribute to Spark
- attend a Spark Meetup
- recruit people with Spark expertise -->


[rise]: http://www.slideshare.net/SparkSummit/riselab-enabling-intelligent-realtime-decisions-keynote-by-ion-stoica
[matei]: https://www.slideshare.net/SparkSummit/trends-for-big-data-and-apache-spark-in-2017-by-matei-zaharia