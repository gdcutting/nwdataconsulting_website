---
title: "Nested Data"
date: 2023-08-08T12:25:02-07:00
draft: true
author: "Guy Cutting"
category: "In Practice"
tags: ["Nested Data", "Google BigQuery", "Google Cloud", "Google Analytics", "Spark"]
---

I've written recently about nested data in a (historically-oriented) discussion of the Parquet format, which is linked to Google's Dremel product and has, as one of its strong points, the ability to work with nested data...

In the bit picture, we often categorize data as unstructured, semi-structured, and structured. Nested data is structured data, because nesting involves adding additional structure to the main data structure. Where does nested data enter the picture? There are a couple of answers to this question:

- some data lends itself to a nested representation. As we'll see with the Google Analytics data discussed in this article, web analytics are a prime example for nesting because each record involves several fields which are themselves best represented as records...

A record with a nested structure might look like (from the Google Analytics example) like this. Not that for brevity I am not enumerating the whole data structure (you can find that at [this Google data dictionary record](https://support.google.com/analytics/answer/3437719?hl=en))

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

This Google Analytics data is an excellent example of a nested dataset (and why you might want to choose to structure your data this way). Each event record contains multiple RECORD fields, and some of these (like ```device```), further contains a RECORD type (so the nesting on this field goes three levels deep). As you can see from this example, one of the advantages of nested data is that it very naturally conveys hierarchical relationships. T

From a data engineering perspective, nested data has some distinct advantages...

The nested approach is not the only way to structure this data. Instead of including event params, devices, items and other fields as a nested RECORD, we could store them each in their own separate tables with relevant foreign keys so that the tables could be linked together in a join query... But think about what this other hypothetical data model (in which the data is highly **[normalized](https://en.wikipedia.org/wiki/Database_normalization)** would mean in terms of accessing the data. In the above nested format, one record from one table includes all of the information about a single event, across multiple dimensions (several of which are RECORDs with their own internal structure); in a non-nested, normalized version, getting full information about an event would requring linking together multiple tables through foreign keys, which would require non-trivial logic to link the tables together correctly...

A proponent of the normalized approach would say that despite the additional overhead and complexity from normalizing the data, the approach is still better because conceptually it treats separate objects as separate data entities with their own tables, and that this helps to enforce data integrity. One drawback with nested data is always that when you de-normalize you are possibly introducing redundancy. Having ```device``` as a nested sub-record in the analytics events table means that there will often be multiple redundant entries for the same device. An active mobile phone user who is browsing the web on their phone might generate a couple of dozen google analytics events in an hour, and each of these event records will include the complete enumeration of their device properties (category, brand name, OS, language, browser info) all over again. If the data was normalized, each unique device could be given its own unique ID, and that ID could be stored by itself in a ```device_id``` column in the events table; then the events table could be linked to a devices table by the ```device_id```...

In some types of data, the logic of eliminating redundancy might be more persuasive. If we were talking, for example, about customer data on an e-commerce site, order information is something that you might not want to normalize, since this could potentially get very complex as customers placed numerous orders over time, and orders themselves have enough distinct properties that they might deserve their own table. E-commerce is still one of the bedrock applications for the time-tested RDBMS model. The logic of normalizing ordern information is still debatable, but I'm using it to make a point here. For the Google Analytics application, we probably care  a lot about the properties of the device at the moment they were recorded, but not much about their historical properties. We're interested in what that phone looked like at the moment that web request was performed; if the user gets a new phone, that will be reflected in different ```device``` properties for future requests will be different, and Google is still storing a more unique ```visitor_id``` field which captures information across multiple devices.

One of my goals for this discussion is to make it clear that the best data model is not always obvious from the application or use case. Particularly with modern datasets which might include large numbers of fields and combinations of structured, raw, and nested data, there might be multiple approaches, with intelligent arguments to be made for competing approaches. At my last salaried job, a proprietary data warehouse had been built in MySQL on top of the application database (this is a [huge architectural anti-pattern](/is-the-data-warehouse-dead/), by the way; **big no-no here**)

https://cloud.google.com/blog/topics/developers-practitioners/bigquery-explained-working-joins-nested-repeated-data