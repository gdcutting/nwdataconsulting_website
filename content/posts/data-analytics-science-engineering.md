---
title: "What's the relationship between data analytics, data science, and data engineering?"
date: 2023-04-11T19:21:44-07:00
draft: false
author: "Guy Cutting"
tags: ["Data", "Data Science", "Data Engineering", "Data Analysis", "Analytics", "ETL", "Data Management"]
---

![Venn Diagram of Data Engineering, Data Science, and Business Stakeholders](/data-scientist-engineer-diagram.png)

This diagram is helpful for visualizing the relationship between data engineering, data science, and the business stakeholders. Thanks to [David Holm on Twitter](https://twitter.com/cloudpreacher). 

A subject that is sometimes the source of ambiguity and confusion is the relationship between data analytics, data science, and data engineering. Increasingly common usage of such terms such as *data analytics engineering*, *business intelligence engineering*, and others can make it even more unclear where the boundaries between these categories and roles actually lie.

*Analytics* can be used in a couple of ways. It is often used in a very general way to refer to the entire process of working with data, from start to finish. In that general sense, *analytics* incorporates data science and data engineering. But *analytics*  can also be used more specifically to refer to the process of building reports from data that has already been ingested and transformed (a process which usually requires several steps.) Thus the *data analyst* role is often restricted to the 'front end' of the process, which involves writing queries that retrieve the appropriate data in the form needed for particular reports.

*Analytics* and *data science* are often used interchangably, and there is quite a bit of overlap, but it is important to understand the differences between the two terms.

Understanding *data engineering* helps put a finer point on the general vs. specific meanings of the term *analytics*. *Data engineering* is concerned with building the data infrastructure required for effective analytics. In this sense, data engineering is necessary to analytics, but is a largely separate area of concern. Data engineers work on the 'back end', meaning the part of the process dealing with the systems for ingesting, storing, processing, and otherwise preparing data for consumption into analytics reports. Data engineers make choices about what tools are necessary for various steps of the process, and how to make them work together. A data engineer might assess a use case and determine that a MySQL database is needed for the application data, that an analytical database like Redshift is needed to store processed data and deliver it for reporting. The data engineer configures these tools and the connections between them, and is also responsible for building the data pipelines which ingest and process data from a raw form into a form which is easily consumable. Tools like [dbt](https://www.getdbt.com/) are used to perform ETL (Extract Transform Load) processes which take raw data (often from multiple disparate sources), and combine and process them through several steps to yield refined data which can more easily be queries by data analysts and scientists.

In an organization with a healthy data culture, these roles are well-defined and each person works in a particular part of the overall data process. Employees in these roles will always work closely together, and sometimes there is crossover between who performs what tasks. But in a well-functioning data culture, the responsibilities of each role are clearly delineated. Ideally, for example, data engineers focus on building infrastructure that processes data to a point where it is readily queryable and consumable by reports built by analysts. 

<br>

One sign of an unhealthy data culture is when the boundaries between roles are murky, and there are not clear expectations about who handles what part of the process. In one case study from my own experience, the data analyst did not have the appropriate skills for the analytical database being used (Redshift). This meant that the data engineer was often asked to write queries for reports, and build the reports in Tableau (tasks which are more properly the responsibility of the analyst). The article [*Engineers Shouldn't Write ETL*](https://multithreaded.stitchfix.com/blog/2016/03/16/engineers-shouldnt-write-etl/) gives some great information about where these boundaries should ideally be drawn.