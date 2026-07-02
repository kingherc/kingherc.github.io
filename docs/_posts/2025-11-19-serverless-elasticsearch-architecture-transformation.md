---
id: 41
title: "Serverless Elasticsearch: The Architecture Transformation from Stateful to Stateless paper at SoCC '25"
date: 2025-11-19T00:00:00+00:00
permalink: /archives/41
categories:
  - Technology
---
I am excited to share our latest paper publication, titled ["Serverless Elasticsearch: The Architecture Transformation from Stateful to Stateless"](https://doi.org/10.1145/3772052.3772245), presented at the [2025 ACM Symposium on Cloud Computing (SoCC '25)](https://acmsocc.org/2025/) research conference. This industrial paper explores a fundamental shift in how we approach distributed search and analytics engines like Elasticsearch.

## Abstract

> Elasticsearch (ES) is a distributed search and analytics engine consisting of a cluster of nodes, each hosting a disjoint subset of data. ES has a shared-nothing architecture that relies on local disks to store cluster data such as index files, transaction logs, and cluster state metadata. This stateful architecture couples compute with storage, and leads to different data tiers (e.g., hot, warm, cold, frozen) of hardware and configurations that the administrator chooses from to balance cost, performance, and high availability. In this paper, we show a new serverless architecture that decouples compute from storage. Serverless ES offloads data to an affordable, highly available cloud object store, while supporting the same APIs and read-after-write semantics. We show why and how this stateless architecture simplifies the tiers to just two: indexing and search, allowing indexing and searching practically limitless data while scaling each tier independently. We describe how we wrap index data in a custom batch commit format to the object store to decrease upload costs by up to 100x, how we batch transaction log uploads to decrease upload costs by up to 30x, and how we delete files from the object store. We experimentally show that Serverless ES can get twice the indexing throughput of (stateful) ES on comparable compute hardware by using object storage for durability instead of replication, and can scale linearly to match ingestion workloads.

## Authors & Acknowledgments

This work was a collaborative effort with: Iraklis Psaroudakis, Pooya Salehi, Jason Bryan, Francisco Fernández Castaño, Brendan Cully, Ankita Kumar, Henning Andersen, and Thomas Repantis. Thank you all for your hard work in making this paper happen!

## Resources

For more context on the paper, please check out our related [Elastic Labs blog post](https://www.elastic.co/search-labs/blog/elasticsearch-serverless-stateless-architecture), which also contains an accessible, downloadable, link of the paper pre-print. You can also download the pre-print version of the paper [here](/assets/posts/2025-11-19-serverless-elasticsearch-architecture-transformation/socc25-p217-preprint.pdf).
