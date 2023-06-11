---
id: 36
title: Elasticsearch presentation at Devoxx Greece 2023
date: 2023-06-11T00:26:16+01:00
permalink: /archives/36
youtubeId: RjbFpjIBtOw
categories:
  - Technology
---
In May 2023 the first ever [Devoxx Greece](https://devoxx.gr/) took place over 3 days, with 60+ speakers, 70+ sessions and 1000+ attendees, in the Athens Megaron International Conference Center. It was an honor to be one of the speakers!

[My presentation](https://devoxx.gr/talk/?id=5252) was titled "Finding needles in ever increasing haystacks - Scalability with Elasticsearch". The abstract of the presentation is:

> The Elastic Stack tackles modern-day observability & security demands of fast-paced searches in ever-increasing data volumes. Elasticsearch, sitting at the core of the Elastic Stack, is a leading distributed search and analytics engine. In this talk, we give an overview of what makes Elasticsearch distributed, efficient and resilient both on bare-metal and on the cloud. This includes an overview of advancements made in recent years. You will learn how: (a) data is ingested, sharded and replicated, (b) searches and aggregations are distributed, (c) recovery works in the event of failures. We conclude with the serverless cloud vision of Elasticsearch for unparallel scalability.

You can access the video recording of the presentation [here](https://www.youtube.com/watch?v=RjbFpjIBtOw&list=PLRsbF2sD7JVpbq0m2mUKFmR-JUgaGwuF-&index=66):

<!-- [![presentation](https://img.youtube.com/vi/RjbFpjIBtOw/maxresdefault.jpg)](https://www.youtube.com/watch?v=RjbFpjIBtOw&list=PLRsbF2sD7JVpbq0m2mUKFmR-JUgaGwuF-&index=66) -->

{% include youtube-embed.html id=page.youtubeId %}

<br />

The slides of the presentation are available [here](/assets/posts/2023-06-11-devoxx-greece-elasticsearch-presentation/2023.05.06.devoxx.greece.elasticsearch.pdf) to download in PDF format.

The agenda of the presentation revolves around the topics:

* What is Elastic.
* What is Elasticsearch, Apache Lucene and inverted indices.
* How Elasticsearch scales out with primary and replica shards.
* How distributed searches & aggregations are executed on multiple machines.
* Shard recovery when a machine fails.
* How core information metadata on cluster state is coordinated wtih consensus across the cluster machines.
* Scaling with data streams for append-only time series data.
* Scaling with Index Lifecycle Management (ILM) across tiers of data nodes with different cost/performance characteristics.
* Future vision on scaling with serverless.

More videos from Devoxx Greece 2023 are available on their [Youtube playlist](https://www.youtube.com/playlist?list=PLRsbF2sD7JVpbq0m2mUKFmR-JUgaGwuF-), and photos from the event on Flickr ([1](https://www.flickr.com/photos/bejug/albums/72177720308364130), [2](https://www.flickr.com/photos/bejug/albums/72177720308379813), [3](https://www.flickr.com/photos/bejug/albums/72177720308381373)).

Enjoy and feel free to share your feedback!