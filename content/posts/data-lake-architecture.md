---
title: "Data Lake Architecture"
date: 2023-08-03T00:02:13-07:00
draft: true
author: "Guy Cutting"
category: ["Data Architecture"]
tags: ["Data Management", "Data Lake"]
---

In this article, Part 2 in a series on **The Evolution Of Data Architectures**, we'll take a look at the **Data Lake**, a newer alternative to the Data Warehouse which is designed to address some of the limitation of that older architecture, which (as part 1 in the series explained) is definitely showing its age and failing to deliver for many companies. See also:

**[Part 1: Is the Data Warehouse Dead?](/is-the-data-warehouse-dead)**

## What is the Data Lake?

Let's first define the term **Data Lake**, especially since not as many readers might be familiar with it. This description is from the [DataBricks](https://www.databricks.com) site:

>A data lake is a central location that holds a large amount of data in its native, raw format. Compared to a hierarchical data warehouse, which stores data in files or folders, a data lake uses a flat architecture and object storage to store the data.‍ Object storage stores data with metadata tags and a unique identifier, which makes it easier to locate and retrieve data across regions, and improves performance. By leveraging inexpensive object storage and open formats, data lakes enable many applications to take advantage of the data.


## What Issues Does Lake Architecture Address

This definition highlights some differences with data warehouses: data

- open storage format. Data lakes use open formats based on cloud storage, rather than the proprietary (closed) formats used by warehouses
- data lakes store data in a raw (unstructured) format, unlike warehouses which deal almost exclusively with structured data

## What Are The Shortcomings of Data Lake

The data lake architecture certainly represents an update on the data warehouse, since many of its architectural elements are intended specifically to address issues with the data warehouse model...

"Many data teams wish to deploy streaming pipelines to ETL or aggregate data in real time, but traditional cloud data lakes are difficult to use for this purpose."

The Data Lake and Hadoop are closely tied together; you can implement data lakes using tools other than Hadoop, but the model of using HDFS (Hadoop File System) as an open format for data lake storage which can store data using cloud-based object storage. From **[this page on processing unstructured data](https://www.ovaledge.com/blog/processing-unstructured-data)**,

>Hadoop was invented to process unstructured data. First at Google, then at Yahoo and Bing, it was used to create page rank based on keywords from the text on the pages. But till date, most of the practical use cases of Hadoop are only to offload ETL from proprietary databases to Hadoop or create new ETL. The reason is that not many people know how to process unstructured data. They are unaware of the kind of insights unstructured data can provide.)

*Unstructured* and *raw* are often used as synonyms when discussing data. Unstructured or raw data is data that is not arranged according to a preset scheme. An example might be weather sensor data. Each individual data record might be small, with just two or three pieces of information: a sensor id, measurement type (temperature, pressure, etc.), and a reading. There would be multiple types of measurement data streaming in at high velocity. While the data is raw, it has enough information to reconstruct a fuller picture of the data, and to build up a more structured model of it would allow more robust querying to retrieve the desired (refined) data..,