---
id: 40
title: "Elasticsearch Serverless: the Transition from Stateful to Stateless presentation at Devoxx Greece 2025"
date: 2025-04-12T00:00:00+03:00
permalink: /archives/40
youtubeId: XQmbTpXfcvo
categories:
  - Technology
---
In April 2025, [Devoxx Greece](https://devoxx.gr/) hosted another successful event in the Athens Megaron International Conference Center. It was an honor to be again one of the speakers!

My presentation was titled "Elasticsearch Serverless: the Transition from Stateful to Stateless". The abstract of the presentation is:

> Modern-day observability & security demand fast-paced searches in ever-increasing data volumes. Elasticsearch (ES), at the core of the Elastic Stack, is a leading distributed AI search and analytics engine. ES has been stateful so far, using primarily the disk to store data. In this presentation, we show the technical design of the new ES Serverless (ES3) mode, that achieves unparalleled scalability without any administration burden. We focus on the basic premise of decoupling compute from storage, and offloading data to an affordable highly available object store (e.g., S3), while supporting the same APIs and read-after-write semantics. Specifically, we show why and how we simplify node tiers to just two: indexing and search. We describe how we use batched compound commits to wrap Lucene files onto the object store, how the translog is buffered on the object store for recovery, and how refresh and search semantics operate.

You can access the video recording of the presentation [here](https://www.youtube.com/watch?v=XQmbTpXfcvo&list=PLRsbF2sD7JVrfxNj1g0OASrT-z9a8avIY&index=48):

<!-- [![presentation](https://img.youtube.com/vi/XQmbTpXfcvo/maxresdefault.jpg)](https://www.youtube.com/watch?v=XQmbTpXfcvo&list=PLRsbF2sD7JVrfxNj1g0OASrT-z9a8avIY&index=48) -->

{% include youtube-embed.html id=page.youtubeId %}

<br />

The slides of the presentation are available [here](/assets/posts/2025-04-12-devoxx-greece-elasticsearch-serverless-presentation/2025.04.12.devoxx.gr.elasticsearch.serverless.pdf) to download in PDF format.

<div style="float: right; width: 30%; margin-left: 2%;">
    <img src="/assets/posts/2025-04-12-devoxx-greece-elasticsearch-serverless-presentation/dD_5284.jpg" alt="Presentation Image">
    <p style="font-size: x-small; line-height: 1.3; color: grey">Posted on <a href="https://www.flickr.com/photos/bejug/54455798865/in/album-72177720325140944">Flickr</a>, by Devoxx Belgium, titled "dD_5284", under an album titled "Devoxx Greece 2025 - Day 3", on 2025-04-16, licensed under <a href="https://creativecommons.org/licenses/by-nc-nd/2.0/deed.en">CC BY-NC-ND 2.0 license</a>.</p>
</div>

The agenda of the presentation revolves around the topics:

* What is Elastic
* What is Elasticsearch
* Shared-nothing stateful architecture
* Serverless Elasticsearch
* New stateless architecture
* Walkthrough of how data is stored in stateful vs serverless Elasticsearch
* Batching data
* Autoscaling

More videos from Devoxx Greece 2025 are available on their [Youtube playlist](https://www.youtube.com/playlist?list=PLRsbF2sD7JVrfxNj1g0OASrT-z9a8avIY), and photos from the event on Flickr ([1](https://www.flickr.com/photos/bejug/albums/72177720325111958/with/54453523809), [2](https://www.flickr.com/photos/bejug/albums/72177720325103936), [3](https://www.flickr.com/photos/bejug/albums/72177720325140944/)).

Enjoy and feel free to share your feedback!