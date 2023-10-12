---
title: "Delta Lake Deeper Dive"
date: 2023-08-03T05:40:02-07:00
draft: true
author: "Guy Cutting"
category: ["Data Architecture"]
tags: ["Data Management", "Data Lake", "Data Warehousing", "DataBricks", "Computer Science", "Cloud Storage", "Whitepapers"]
---

In recent posts I've been exploring [DataBricks](https://databricks.com) and their products, which represent a powerful new approach to data management. Here are a couple of those recent articles:

- **[Is DataBricks and Delta Lake Right For You?](/is-databricks-delta-lake-right-for-you)**
- **[DataBricks Resources for Practitioners, Managers, and Decision-Makers](/databricks-resources)**

Having worked on a couple of projects with the DataBricks cloud data processing platform and really enjoying the experience, I'm now taking a deeper dive into DataBricks' offerings, which are comprehensive, including:

- the **lakehouse** architecture which builds on the data lake and addresses some of the shortcomings of that architecture, including
- the **Delta Lake** ([GitHub repo](https://github.com/delta-io)) open source storage layer, which uses object-based cloud storage and adds numerous features such as ACID transactions, a transaction log that enables time travel and fast metadata operations, data layout optimization, caching, and audit logs. Delta Lake tables can be accessed from common tools like Spark, Hive, Presto, Redshift, and others. 
- the DataBricks cloud service which runs on multiple cloud vendors and allows users to build comprehensive data platforms to do high-performance analytics and machine learning without requiring them to learn cloud specific tools and processes.

In this article I'd like to focus on the **Delta Lake** storage layer, which represents one of the major innovations in the data space in recent years. DataBricks is closely tied to [Apache Spark](https://www.apache.org/spark), with several of their founders having founded and worked on the Spark project. You don't have to know anything about the technical details of Delta Lake to use the DataBricks cloud platform, but one of the standout points about DataBricks (the company) is that they embrace open source, and provide a great deal of detail about their Delta Lake framework. For more technically minded readers, it's worth taking a deeper dive into Delta Lake to understand what's under the hood, so that you can truly take advantage of all the platform has to offer. 

[open format - Parquet]