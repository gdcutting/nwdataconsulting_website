---
title: "BigQuery Part 1: Getting Started"
date: 2020-04-23T20:08:17-07:00
draft: false
tags: ["Google Cloud Platform", "Cloud", "BigQuery", "SQL", "Python", "Big Data"]
categories: ["Data Science"]
---

BigQuery, one of the many services available on Google Cloud Platform, is an enterprise data warehouse which lets you perform fast queries on very large datasets using Google's infrastructure. You can get started using it free of charge with one of the many publicly available datasets built into GCP.

In this installment, we'll take a look at setup and basic usage. I put together a jupyter notebook to demonstrate. The 'Open in Colab' link will take you to the Colaboratory interactive version which will run in your browser. You might also need to use that link if the Gist embed below isn't working (notebook embeds have been occasionally acting up on Gist lately).


<a href = "https://colab.research.google.com/github/gdcutting/bigquery/blob/master/Google_BigQuery_Getting_Started.ipynb" target = "new">View this notebook on Google Collaboratory</a>

# Getting started with the BigQuery API

We want to start exploring the Google BiqQuery [public datasets](https://cloud.google.com/bigquery/public-data/). Let's start by walking through the required setup steps, and then we can load and explore some data. Note that the procedure for using BigQuery outside of the colaboratory notebook environment is different and will be described in a separate article.

## Preliminaries
Follow [this quickstart guide](https://cloud.google.com/bigquery/docs/quickstarts/quickstart-client-libraries), which will explain how to:

1. Create a [Cloud Platform project](https://console.cloud.google.com/cloud-resource-manager) if you don't have one already.
2. [Enable billing](https://support.google.com/cloud/answer/6293499#enable-billing)) for the project
3. [Enable the BigQuery API](https://console.cloud.google.com/flows/enableapi?apiid=bigquery)

#### Provide credentials to the runtime
Now we need to authenticate to gain access to the BigQuery API. When you first run this, you will be given a link to a page with your authentication key, which you will need to paste here.

```python
from google.colab import auth
auth.authenticate_user()
print('Authenticated')
```

Now that we're authenticated, we need to load the BigQuery package
, and the google.colab.data_table package that can be used to display large pandas dataframes as an interactive data. Loading data_table is optional, but it will be useful for working with data in pandas.

```python
%load_ext google.cloud.bigquery
%load_ext google.colab.data_table
```

## Typical API Usage (through google-cloud-bigquery)

Now we can create a client, specifying the project name (replace 'bigquery-test-project-256220' with your project name, which you can find in the [GCP console](https://console.cloud.google.com))

```python
project_id = '[bigquery-test-project-256220]'
client = bigquery.Client(project_id)
```

With the client created for our project, now we can set up dataset references for a couple of datasets, Hacker News and [Bitcoin](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=crypto_bitcoin&page=dataset&project=bigquery-test-project-256220&folder&organizationId) datasets.

[See the full list of public datasets](https://console.cloud.google.com/marketplace/browse?filter=solution-type:dataset) if you want to explore others.

```python
hn_dset_ref = client.dataset('hacker_news', project='bigquery-public-data')
bc_dset_ref = client.dataset('crypto_bitcoin', project='bigquery-public-data')
```

Now that we have data *references*, we can load the actual datasets and confirm the type.

```python
hn_dset = client.get_dataset(hn_dset_ref)
bc_dset = client.get_dataset(bc_dset_ref)
type(bc_dset)
```

<pre> google.cloud.bigquery.dataset.Dataset</pre>

Use client.list_tables, along with [list comprehension](https://www.python.org/dev/peps/pep-0202/), to get table information for both datasets:

```python
print([t.table_id for t in client.list_tables(hn_dset)])
print([t.table_id for t in client.list_tables(bc_dset)])
```

<div>
Output:
<pre>
['comments', 'full', 'full_201510', 'stories']
['blocks', 'inputs', 'outputs', 'transactions']
</pre>
</div>

Let's take a closer look at the 'blocks' table in the bitcoin dataset:

```python
bc_blocks = client.get_table(bc_dset.table('blocks'))
[command for command in dir(bc_blocks) if not command.startswith('_')]
```


<div>
Output:
<pre>
['clustering_fields',
 'created',
 'dataset_id',
 'description',
 'encryption_configuration',
 'etag',
 'expires',
 'external_data_configuration',
 'friendly_name',
 'from_api_repr',
 'from_string',
 'full_table_id',
 'labels',
 'location',
 'modified',
 'num_bytes',
 'num_rows',
 'partition_expiration',
 'partitioning_type',
 'path',
 'project',
 'reference',
 'schema',
 'self_link',
 'streaming_buffer',
 'table_id',
 'table_type',
 'time_partitioning',
 'to_api_repr',
 'to_bqstorage',
 'view_query',
 'view_use_legacy_sql']
 </pre>
 </div>

Let's examine the schema to get more information:

```python
bc_blocks.schema
```

<div>
Output:
<pre>
[SchemaField('hash', 'STRING', 'REQUIRED', 'Hash of this block', ()),
 SchemaField('size', 'INTEGER', 'NULLABLE', 'The size of block data in bytes', ()),
 SchemaField('stripped_size', 'INTEGER', 'NULLABLE', 'The size of block data in bytes excluding witness data', ()),
 SchemaField('weight', 'INTEGER', 'NULLABLE', 'Three times the base size plus the total size. https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki', ()),
 SchemaField('number', 'INTEGER', 'REQUIRED', 'The number of the block', ()),
 SchemaField('version', 'INTEGER', 'NULLABLE', 'Protocol version specified in block header', ()),
 SchemaField('merkle_root', 'STRING', 'NULLABLE', 'The root node of a Merkle tree, where leaves are transaction hashes', ()),
 SchemaField('timestamp', 'TIMESTAMP', 'REQUIRED', 'Block creation timestamp specified in block header', ()),
 SchemaField('timestamp_month', 'DATE', 'REQUIRED', 'Month of the block creation timestamp specified in block header', ()),
 SchemaField('nonce', 'STRING', 'NULLABLE', 'Difficulty solution specified in block header', ()),
 SchemaField('bits', 'STRING', 'NULLABLE', 'Difficulty threshold specified in block header', ()),
 SchemaField('coinbase_param', 'STRING', 'NULLABLE', 'Data specified in the coinbase transaction of this block', ()),
 SchemaField('transaction_count', 'INTEGER', 'NULLABLE', 'Number of transactions included in this block', ())]
 </pre>
 </div>

 The table scheme gives us column names, types, parameters, descriptions, and (for the weight, a link to a GitHub repo).

 The schema is a necessary input for one of the more common and useful [BigQuery commands](https://googleapis.dev/python/bigquery/latest/reference.html): `list_rows()`, which returns a slice of the dataset without scanning any other section of the table. For that reason, it is often preferable to using a `limit` clause in your query.

 We want to select a subset of the columns, but the `selected_fields` parameter requires a schema object as an input, so we need to build a subset of the schema first to pass for that parameter.

```python
schema_subset = [col for col in bc_blocks.schema if col.name in ('number', 'timestamp', 'hash')]
results = [x for x in client.list_rows(bc_blocks, start_index=100, selected_fields=schema_subset, max_results=10)]
```

Let's take a look at the results, first in raw format (not very easy to look at), then in dictionary form (much neater):

```python
print(results)
for i in results:
    print(dict(i))
```

<div>
Output:
<pre>
[Row(('000000000000000000824a2cbabfd94ded8a80c4179a9e662eebb205a6d22663', 487527, datetime.datetime(2017, 9, 29, 14, 25, 30, tzinfo=<UTC>)), {'hash': 0, 'number': 1, 'timestamp': 2}), Row(('0000000000000000000030b69821159aeabd59ce42f32d3c0b10dfa3fab984f1', 487001, datetime.datetime(2017, 9, 26, 5, 55, 18, tzinfo=<UTC>)), {'hash': 0, 'number': 1, 'timestamp': 2}), Row(('000000000000000000f6f0d7f30bb0c820b20c0a238d6b13747fb34b1ffda97d', 487132, datetime.datetime(2017, 9, 27, 2, 47, 7, tzinfo=<UTC>)), {'hash': 0, 'number': 1, 'timestamp': 2}), Row(('000000000000000000d0eaefb69506912073c17d0388727bd3c1463ecd2ad2a2', 486707, datetime.datetime(2017, 9, 24, 0, 58, 8, tzinfo=<UTC>)), {'hash': 0, 'number': 1, 'timestamp': 2}), Row(('0000000000000000007908cf4cab8d18b29bd5aa2b292a414f6c10675f9984eb', 487282, datetime.datetime(2017, 9, 28, 3, 58, 8, tzinfo=<UTC>)), {'hash': 0, 'number': 1, 'timestamp': 2}), Row(('000000000000000000e330bef17e39727e0ead7bce9b82f57b871be23add429e', 487003, datetime.datetime(2017, 9, 26, 6, 17, 5, tzinfo=<UTC>)), {'hash': 0, 'number': 1, 'timestamp': 2}), Row(('0000000000000000008820077a37573e5a3c0d6a8315513e4cccd59462771228', 485973, datetime.datetime(2017, 9, 19, 3, 12, 9, tzinfo=<UTC>)), {'hash': 0, 'number': 1, 'timestamp': 2}), Row(('00000000000000000000133426bc20b82bb1827108a626db6bde3c45adf93824', 486014, datetime.datetime(2017, 9, 19, 11, 19, 41, tzinfo=<UTC>)), {'hash': 0, 'number': 1, 'timestamp': 2}), Row(('00000000000000000073100b1b3cb9ed537c43666a39e388f86e4484e7c14e30', 486192, datetime.datetime(2017, 9, 20, 20, 1, 14, tzinfo=<UTC>)), {'hash': 0, 'number': 1, 'timestamp': 2}), Row(('0000000000000000000f9bc1d8095de15900a39db25b8323c71985778626a1e8', 487118, datetime.datetime(2017, 9, 27, 1, 15, 14, tzinfo=<UTC>)), {'hash': 0, 'number': 1, 'timestamp': 2})]
{'hash': '000000000000000000824a2cbabfd94ded8a80c4179a9e662eebb205a6d22663', 'number': 487527, 'timestamp': datetime.datetime(2017, 9, 29, 14, 25, 30, tzinfo=<UTC>)}
{'hash': '0000000000000000000030b69821159aeabd59ce42f32d3c0b10dfa3fab984f1', 'number': 487001, 'timestamp': datetime.datetime(2017, 9, 26, 5, 55, 18, tzinfo=<UTC>)}
{'hash': '000000000000000000f6f0d7f30bb0c820b20c0a238d6b13747fb34b1ffda97d', 'number': 487132, 'timestamp': datetime.datetime(2017, 9, 27, 2, 47, 7, tzinfo=<UTC>)}
{'hash': '000000000000000000d0eaefb69506912073c17d0388727bd3c1463ecd2ad2a2', 'number': 486707, 'timestamp': datetime.datetime(2017, 9, 24, 0, 58, 8, tzinfo=<UTC>)}
{'hash': '0000000000000000007908cf4cab8d18b29bd5aa2b292a414f6c10675f9984eb', 'number': 487282, 'timestamp': datetime.datetime(2017, 9, 28, 3, 58, 8, tzinfo=<UTC>)}
{'hash': '000000000000000000e330bef17e39727e0ead7bce9b82f57b871be23add429e', 'number': 487003, 'timestamp': datetime.datetime(2017, 9, 26, 6, 17, 5, tzinfo=<UTC>)}
{'hash': '0000000000000000008820077a37573e5a3c0d6a8315513e4cccd59462771228', 'number': 485973, 'timestamp': datetime.datetime(2017, 9, 19, 3, 12, 9, tzinfo=<UTC>)}
{'hash': '00000000000000000000133426bc20b82bb1827108a626db6bde3c45adf93824', 'number': 486014, 'timestamp': datetime.datetime(2017, 9, 19, 11, 19, 41, tzinfo=<UTC>)}
{'hash': '00000000000000000073100b1b3cb9ed537c43666a39e388f86e4484e7c14e30', 'number': 486192, 'timestamp': datetime.datetime(2017, 9, 20, 20, 1, 14, tzinfo=<UTC>)}
{'hash': '0000000000000000000f9bc1d8095de15900a39db25b8323c71985778626a1e8', 'number': 487118, 'timestamp': datetime.datetime(2017, 9, 27, 1, 15, 14, tzinfo=<UTC>)}
</pre>
</div>

What if we had performed a full table scan, instead of using list_rows? How many resources would have been consumed? Let's find out:

```python
BYTES_PER_GB = 2**30
bc_blocks.num_bytes / BYTES_PER_GB
```

### Using BiqQuery via magics

There's another, shorthand way to access data (replace 'bigquery-test-project-256220' with your project ID):

```python
%%bigquery --project bigquery-test-project-256220
SELECT
  COUNT(*) as total_rows
FROM `bigquery-public-data.crypto_bitcoin.blocks`
```

![Bitcoin query results](/images/bq-table-1.png)

Here's the whole notebook as a gist. Click the link at the top to view in Google Colab, so that you can run it interactively:

<style type="text/css">
  .gist {width:100%; overflow:auto}  
  .gist .file-data {max-height: 1000px;max-width: 500px;}
</style>

<script src="https://gist.github.com/gdcutting/92322a5717cefa556047e76f1529f655.js"></script>
