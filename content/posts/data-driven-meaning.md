---
title: "What does it mean to be 'data-driven'?"
date: 2023-04-12T17:59:56-07:00
draft: false
author: "Guy Cutting"
---

## Introduction

One of the many great resources for me on my professional journey has been the book [*Creating A Data-Driven Organization*](https://www.oreilly.com/library/view/creating-a-data-driven/9781491916902/), by Carl Anderson. I would recommend it for anyone who's involved in working with data, from managers and executives, to analysts, scientists, engineers and others.

## Prerequisites
The first line of Anderson's book is that "Data-drivenness is about building tools, abilities, and, most crucially, a culture that acts on data." In explaining further what it means to be data-driven, Anderson defines a few prerequisites:

- *1. An organization must be collecting data.* This isn't as easy as it sounds, because of course you must be collecting the *right* data. Data has to be timely, accurate, clean, unbiased, and trustworthy. Getting high-quality data can be a lot of work. Raw data is often messy and requires cleaning - one oft-cited estimate states that data scientists spend roughly 80% of their time cleaning data and only 20% of their time building models, analyzing, and drawing conclusions. A small amount of high-quality data can be more actionable that a large quantity of junk data, so it's important to know the difference. I once worked with a company that had a daily report on the number of new application users. It turned out, after some investigation, that the timestamp value that the analytics used to determine the day on which jobs were posted was often incorrectly updated by an errant application process. So although this company had an automated report in place to monitor daily new users, the results of that report were often wildly misleading because no one had taken the time to understand how the raw data was being handled. Making decisions based on inaccurate data can give a false sense of security, and be worse than not having analytics to begin with.

- *2. Data must be accessible and queryable.* The data must be able to be joined to other enterprise data when necessary. This requires the right choice of tool - relational database, NoSQL, or maybe something else. Anderson cites a case study in which a company was spending a huge amount of time analyzing their data because it was all in Excel spreadsheet form. I have experienced this exact situation first-hand, working with an organization that started its analytics process by collecting data by hand from the web application and putting it into spreadsheets. The process was tedious, and this inefficiency drastically limited the amount of data they could analyze. For that company, an important first step was automating the warehousing of data into Redshift (the AWS analytical database service) so that it all existed in one place (instead of multiple spreadsheets) and could be queried using SQL. This was in 2022, but this particular organization was still analyzing its data in a way that was common twenty years earlier, meaning that it was failing to take advantages of the tremendous advances in analytics tools that have taken place in the last two decades. This sort of situation is surprisingly common.

- *3. You need people with the right skills to use the data.* Having the right data, and storing it in the right way, is still not enough to get the best insights from that data. Your data analysts or scientists must have the appropriate skills to use the data that you have. In the case study discussed under #2 above, the company was limited by the fact that their single data analyst knew some SQL, but had no experience with Redshift, the database service they were using. So even once the data engineer built a solution to ingest the data into Redshift, the analytics process was still hobbled because the analyst wasn't proficient with Redshift SQL. One of the reasons for this issue was that, although the analyst was eager to learn Redshift, for many months she had spent all of her time compiling data into spreadsheets and performing analysis by hand, meaning that she had no time left to learn the more important skill of querying the data from Redshift.

The above points all sound simple, but the devil is in the details. Many if not most organizations struggle with relatively basic technical and organizational limitations such as those described in the above case studies. And these point describe merely the first step in taking advantage of your data - if you don't have quality data that's accessible by your employees with their current skills, how can you hope to build a robust analytics culture that continually provides meaningful insights into your data?

<br>

## Hallmarks

Anderson goes on to describe several hallmarks of data-driven organizations to help assess the state of an organization's analytics efforts:

- Data-driven organizations usually perform frequent testing, such as A/B testing to measure the relative effectiveness of different email subject lines in a marketing campaign. 
- Such organizations must not merely be backward-looking. Most common types of analytics provide reporting and alerts about past data. But effective decision-making is concerned not only with the past, but what will likely happen in the future. Data-driven organizations are often involved in *predictive* modeling that provides well-informed estimates of future behavior. 
- These organizations usually have a mindset of continuous improvement. An effective analytics culture takes the approach that ongoing development is always required to maintain a high level of insight from data, rather than thinking that, once in place, a certain system or set of reports will provide all the insight needed from ongoing data operations.
- Data-driven organizations will provide analysis to the correct decision-makers, who will use it as critical evidence to help inform and influence strategy. The most sophisticated analysis in the world is of little use if the right managers and executives don't have easy access to it, and know how to use it to make critical decisions. This point, once again, might sound simplistic, but it is of crucial importance, and often overlooked. Every link in the analytics and decision-making value chain must be strong, or your organization will still fail to make the best use of its data.

Of course there's much more to creating a powerful data culture. After all, Anderson and many others have written entire books on the subject. But this overview gives you some idea of the most important issues at play in developing that culture. Oftentimes it is the most basic, and easy to make, mistakes that are the most crippling to effective data-driven decision making.

I'm here to help you avoid those mistakes and implement the sound foundational principles of an effective data culture. If you have questions, or to schedule a consultation, [see the contact page](/contact/).