---
title: "Moving to OpenSearch"
date: 2019-12-20T15:44:46+06:00
type: portfolio
image: "images/projects/project-thumb-four.jpg"
category: "FAQ"
tags: ["FAQ"]
toc: true
project_images: ["images/projects/project-details-image-one.jpg", "images/projects/project-details-image-two.jpg"]
---

> This FAQ explains some of the reasons for moving a software product based on Open Distro to OpenSearch. It was meant to serve as a guide to understand the need for the changes and the steps necessary to upgrade the software components. 

# FAQ: Moving to OpenSearch

## Why is ACME moving away from Open Distro?

The release in 2010 of Elasticsearch marked a significant milestone in the world of search and data analytics. It offered a distributed, open-source, full-text search and analytics engine designed for multitenancy and scalability. For that reason, ACME quickly adapted the technology and released its own ACME Elasticsearch Framework. That framework was developed and maintained for Universes 9.4, 10.0, 11.0, 11.1, 11.2 and 11.3.

In early 2021, Elasticsearch announced changes in its licensing model and imposed restrictions that made ACME move on to Open Distro for Elasticsearch (ODFE). At the time, Open Distro offered a solid alternative with seamless compatibility and extended security features. Therefore, as part of Universe 12.0, ACME released his own Open Distro Operator, an ecosystem of tools that allowed users to easily operate an Elasticsearch cluster with enterprise capabilities in the cloud.

As of May 2022, the open-source Elasticsearch reached its end of life. For that reason, the Open Distro project became unsustainable and https://opendistro.github.io/for-elasticsearch/[all users were encouraged to migrate to OpenSearch]. OpenSearch is a fully open-source project in production since 2021 that is developing under an https://www.apache.org/licenses/LICENSE-2.0[Apache License (Version 2.0)]. From universe 13.0, ACME released an OpenSearch Operator, ensuring the technology’s continuity in the platform.

## What elements of ACME use OpenSearch?

OpenSearch is used in the Governance search engine, in the centralized logging and as a standalone component in ACME Search.

## Should I migrate to the OpenSearch Operator?


| Upgrade               |                                                            |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| From 11.1.0 to 11.3.0 | Upgrade to Elasticsearch framework 2.7.0 and Elasticsearch security agent 2.3.9 through the usual process via the application manager. The product logs solution and the searcher are integrated with Elasticsearch. |
| From 11.3.0 to 13.1   | Upgrade to OpenSearch 0.2.3 and OpenSearch security agent 2.4.7. The product’s logs solution is integrated with Open Distro but ACME Search is integrated with OpenSearch. It is not recommended to deploy any Open Distro instances.|
| From 13.1.0 to 14.0   | Upgrade to OpenSearch 0.3.x and OpenSearch security agent 2.5.0. The product’s logs solution and ACME Search are integrated with OpenSearch. The security agent is decoupled and needs to be managed as any other service from the marketplace.|

