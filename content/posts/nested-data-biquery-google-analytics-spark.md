---
title: "Nested Data"
date: 2023-08-08T12:25:02-07:00
draft: true
author: "Guy Cutting"
category: "In Practice"
tags: ["Nested Data", "Google BigQuery", "Google Cloud", "Google Analytics", "Spark"]
---

(is this part 1 in a series or are we gonna do some spark stuff here?)

I've written recently about nested data in a (historically-oriented) discussion of the Parquet format, which is linked to Google's Dremel product and has, as one of its strong points, the ability to work with nested data...

In the bit picture, we often categorize data as unstructured, semi-structured, and structured. Nested data is structured data, because nesting involves adding additional structure to the main data structure. Where does nested data enter the picture? There are a couple of answers to this question:

- some data lends itself to a nested representation. As we'll see with the Google Analytics data discussed in this article, web analytics are a prime example for nesting because each record involves several fields which are themselves best represented as records. This occurs in part because web analytics tracking captures a lot of information at a point in time (when a user interacts with a tagged site) - about the user, the device, the browser...
- oftentimes the data practitioner (probably in this case the data engineer) chooses a nested data model in order to make a more elegant and functional representation of the data. Remember that there is almost always a choice of how to organize data when building an application or processing pipeline - bigger datasets (in terms of number of dimensions) will involve more choices of how to schematize; most modern database platforms support some type of nesting, but BigQuery probably does this better than any other platform.

In other words, nested data enters the picture where using a nested structure makes the most sense, from the underlying data structure (as understood by the DE or analyst), and involving considerations of efficiency and processing overhead. In certain situations, using a nested representation (particularly on BigQuery, where many of its [best optimizations are centered around nested and repeated data](https://cloud.google.com/bigquery/docs/best-practices-performance-nested)) can result in dramatically faster processing, and a good data engineer will learn to recognize when and where to use nested structures for greatest effect in both simplifying the data model and at the same time enabling better query performance for the most common and expensive queries in the intended use case... See also [some best practices for data loading when denormalizing](https://cloud.google.com/bigquery/docs/loading-data#loading_denormalized_nested_and_repeated_data).

A record with a nested structure might look (from the [Google Analytics](https://console.cloud.google.com/marketplace/product/obfuscated-ga360-data/obfuscated-ga360-data?project=bigquery-census-ml) dataset available from [BigQuery Public Datasets](https://cloud.google.com/bigquery/public-data)) like this. By the way, if you haven't taken advantage of the BigQuery Public datasets, you really should check them out. For data exploration and finding some new and interesting data to pipeline and work on for projects, BigQuery has dozens of fantastic datasets that are publicly available. Go check it out. Anyway, back to the Google Analytics data; note that for brevity I am not enumerating the whole data structure (you can find that at [this Google data dictionary record](https://support.google.com/analytics/answer/3437719?hl=en))

- event name
- event data
- event params (RECORD)
  - key
  - value
    - string_value
    - int_value
    - float_value
    - double_value
- device (RECORD)
    - category
    - mobile_brand_name
    - operating system
    - language
    - web_info (RECORD)
      - browser
      - browser version

This Google Analytics data is an excellent example of a nested dataset (and why you might want to choose to structure your data this way). Each event record contains multiple RECORD fields, and some of these (like ```device```), further contains a RECORD type (so the nesting on this field goes three levels deep). As you can see from this example, one of the advantages of nested data is that it very naturally conveys hierarchical relationships. It is clear just from looking at the data schema that ```browser``` belongs to ```web_info``` which belongs to ```device```...

From a data engineering perspective, nested data has some distinct advantages... The first advantage, from which a lot of other things flow, is simplifying the data model (which means, when it is done appropriately, simplifying *working with* that data). When you introduce the idea of RECORD as a field type, and in this way adding an extra dimensionality to the data structure, it can be intimidating to wrap your head around. One reason that highly normalized data models still persist is that, in some ways, they are the easiest to work with - every logical entity gets its own table, tables are linked through foreign keys, and complex entities are built up by using JOINs to combine tables. This is usually the way people learn to do database development (at least it was for me), so often my natural fallback is just to normalize everything to keep the entities straight and avoid repeating values across tables. And for querying, a lot of people learn JOINs early on in their SQL education, and nested data introduces a slightly different SQL pattern (though one that can be learned in a few minutes).

But the highly normalized data model is not the only one, and in this use case the benefits of using nested structure stand out. Instead of including event params, devices, items and other fields as a nested RECORD, we could store them each in their own separate tables with relevant foreign keys so that the tables could be linked together in a join query... But think about what this other hypothetical data model (in which the data is highly **[normalized](https://en.wikipedia.org/wiki/Database_normalization)** would mean in terms of accessing the data. In the above nested format, one record from one table includes all of the information about a single event, across multiple dimensions (several of which are RECORDs with their own internal structure); in a non-nested, normalized version, getting full information about an event would require linking together multiple tables through foreign keys, which would require non-trivial logic to link the tables together correctly... Building an ```event``` record might require joining half a dozen tables, and this immediately sounds computationally expensive.

A proponent of the normalized approach would say that despite the additional overhead and complexity from normalizing the data, the approach is still better because conceptually it treats separate objects as separate data entities with their own tables, and that this helps to enforce data integrity. One drawback with nested data is always that when you de-normalize you are possibly introducing redundancy. Having ```device``` as a nested sub-record in the analytics events table means that there will often be multiple redundant entries for the same device. An active mobile phone user who is browsing the web on their phone might generate a couple of dozen google analytics events in an hour, and each of these event records will include the complete enumeration of their device properties (category, brand name, OS, language, browser info) all over again. If the data was normalized, each unique device could be given its own unique ID, and that ID could be stored by itself in a ```device_id``` column in the events table; then the events table could be linked to a devices table by the ```device_id```...

In some types of data, the logic of eliminating redundancy might be more persuasive. If we were talking, for example, about data on an e-commerce site, order information is something that you might not want to normalize, since this could potentially get very complex as customers placed numerous orders over time, and orders themselves have enough distinct properties that they might deserve their own table. E-commerce is still one of the bedrock applications for the time-tested RDBMS model. The logic of normalizing order information is still debatable, but I'm using it to make a point here. For the Google Analytics application, we probably care  a lot about the properties of the device at the moment they were recorded, but not much about their historical properties. We're interested in what that phone looked like at the moment that web request was performed; if the user gets a new phone, that will be reflected in different ```device``` properties for future requests will be different, and Google is still storing a more unique ```visitor_id``` field which captures information across multiple devices.

For more details on denormalization, particularly in reference to BigQuery, see the relevant [Google Docs page](https://cloud.google.com/bigquery/docs/migration/schema-data-overview#denormalization). It's interesting that Google emphasizes that,

>BigQuery supports both star and snowflake schemas, but its native schema representation is neither of those two. It uses nested and repeated fields instead for a more natural representation of the data

That's how important nested and repeated data is to the native data representation in BigQuery - it's at the level of another type of architecture entirely. Neither the star or snowflake captures, in the same with, the kind of rich structure that is possible with nested and repeated fields. In appropriate use cases, this makes BigQuery a leader in its category; it's inherently serverless already, so as compared to Redshift (which is only now rolling out a serverless version, more than a decade after the original hit the market), you're not paying for an expensive partially-used cluster, and you get the benefit of rich and robust data structures using data nesting and repeating. In both of these ways, BigQuery was way ahead of the game...

One of my goals for this discussion is to make it clear that the best data model is not always obvious from the application or use case. Particularly with modern datasets which might include large numbers of fields and combinations of structured, raw, and nested data, there might be multiple approaches, with intelligent arguments to be made all around. At my last salaried job, several years ago a proprietary data warehouse had been built in MySQL on top of the application database (this is a [huge architectural anti-pattern](/is-the-data-warehouse-dead/), by the way; **big no-no here**). With the benefit of hindsight, it's easy to see that this was a terrifically bad idea; but at the time a number of very knowledgeable people put their heads together, and that proprietary DW was the result, so there must have been some logic for it.

This GA data is a more nuanced example of that phenomenon in which there are still other viable approaches. But since this is a BigQuery dataset, we would expect it to make use of BigQuery's features for dealing with nested data (which not all data warehouse platforms implement to this extent, or in the same way). Nested data is a standout feature of BigQuery because, when used correctly, it enables a simplified, higher-performing data model.

https://cloud.google.com/blog/topics/developers-practitioners/bigquery-explained-working-joins-nested-repeated-data

(for the spark part, just start with a bunch of counts of different stuff in the event data. get a bunch of records (several gb worth) and look at counts of unique users, devices, etc.)