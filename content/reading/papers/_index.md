---
title: "Reading - Papers"
date: 2023-6-12T03:24:32-07:00
draft: false
author: "Guy Cutting"
categories: ["Reading"]
tags: ["Data Science", "Artificial Intelligence", "Machine Learning", "Research", "Models", "LLMs"]
layout: "single"
---
# Papers (oldest first)

This is a list of important data-related papers (primarily in AI / ML, with some others mixed in):

- [**Dremel: Interactive Analysis of Web-Scale Datasets**](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36632.pdf)
  - Year: 2010
  - Authors: Sergey Melnik, Andrey Gubarev, Jing Jing Long, Geoffrey Romer, Shiva Shivakumar, Matt Tolton, Theo Vassilakis
  - Abstract: 
        {{< details "Dremel is a scalable, interactive ad-hoc query system for analy- sis of read-only nested data..." >}}
            By combining multi-level execution trees and columnar data layout, it is capable of running aggrega- tion queries over trillion-row tables in seconds. The system scales to thousands of CPUs and petabytes of data, and has thousands of users at Google. In this paper, we describe the architecture and implementation of Dremel, and explain how it complements MapReduce-based computing. We present a novel columnar stor- age representation for nested records and discuss experiments on few-thousand node instances of the system.
        {{< /details >}}    
  - DOI: [https://doi.org/10.14778/1920841.1920886](https://doi.org/10.14778/1920841.1920886)
  - Download: [36632.pdf](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36632.pdf)
- [**Attention Is All You Need**](https://arxiv.org/abs/1706.03762) (aka the very influential and important 'The Transformer Paper')
  - Year: 2017
  - Authors: Robert Geirhos, David H. J. Janssen, Heiko H. Schütt, Jonas Rauber, Matthias Bethge, Felix A. Wichmann
  - Abstract: 
        {{< details "The dominant sequence transduction models are based on complex recurrent or convolutional neural networks in an encoder-decoder configuration..." >}}
            The best performing models also connect the encoder and decoder through an attention mechanism. We propose a new simple network architecture, the Transformer, based solely on attention mechanisms, dispensing with recurrence and convolutions entirely. Experiments on two machine translation tasks show these models to be superior in quality while being more parallelizable and requiring significantly less time to train. Our model achieves 28.4 BLEU on the WMT 2014 English-to-German translation task, improving over the existing best results, including ensembles by over 2 BLEU. On the WMT 2014 English-to-French translation task, our model establishes a new single-model state-of-the-art BLEU score of 41.8 after training for 3.5 days on eight GPUs, a small fraction of the training costs of the best models from the literature. We show that the Transformer generalizes well to other tasks by applying it successfully to English constituency parsing both with large and limited training data.
        {{< /details >}}    
  - Download: [1706.03762.pdf](https://arxiv.org/pdf/1706.03762.pdf)
- [**Comparing deep neural networks against humans: object recognition when the signal gets weaker**](https://arxiv.org/abs/1706.06969)
  - Year: 2017
  - Authors: Robert Geirhos, David H. J. Janssen, Heiko H. Schütt, Jonas Rauber, Matthias Bethge, Felix A. Wichmann
  - Abstract: 
        {{< details "The dominant sequence transduction models are based on complex recurrent or convolutional neural networks in an encoder-decoder configuration..." >}}
            The best performing models also connect the encoder and decoder through an attention mechanism. We propose a new simple network architecture, the Transformer, based solely on attention mechanisms, dispensing with recurrence and convolutions entirely. Experiments on two machine translation tasks show these models to be superior in quality while being more parallelizable and requiring significantly less time to train. Our model achieves 28.4 BLEU on the WMT 2014 English-to-German translation task, improving over the existing best results, including ensembles by over 2 BLEU. On the WMT 2014 English-to-French translation task, our model establishes a new single-model state-of-the-art BLEU score of 41.8 after training for 3.5 days on eight GPUs, a small fraction of the training costs of the best models from the literature. We show that the Transformer generalizes well to other tasks by applying it successfully to English constituency parsing both with large and limited training data.
        {{< /details >}}    
  - Download: [1706.03762.pdf](https://arxiv.org/pdf/1706.03762.pdf)
- [**Language Models are Few-Shot Learners**](https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html)
  - Year: 2018
  - Authors: Tom Brown, Benjamin Mann, Nick Ryder, Melanie Subbiah, Jared D Kaplan, Prafulla Dhariwal, Arvind Neelakantan, Pranav Shyam, Girish Sastry, Amanda Askell, Sandhini Agarwal, Ariel Herbert-Voss, Gretchen Krueger, Tom Henighan, Rewon Child, Aditya Ramesh, Daniel Ziegler, Jeffrey Wu, Clemens Winter, Chris Hesse, Mark Chen, Eric Sigler, Mateusz Litwin, Scott Gray, Benjamin Chess, Jack Clark, Christopher Berner, Sam McCandlish, Alec Radford, Ilya Sutskever, Dario Amodei
  - Abstract: 
        {{< details "We demonstrate that scaling up language models greatly improves task-agnostic, few-shot performance, sometimes even becoming competitive with prior state-of-the-art fine-tuning approaches..." >}}
            Specifically, we train GPT-3, an autoregressive language model with 175 billion parameters, 10x more than any previous non-sparse language model, and test its performance in the few-shot setting. For all tasks, GPT-3 is applied without any gradient updates or fine-tuning, with tasks and few-shot demonstrations specified purely via text interaction with the model. GPT-3 achieves strong performance on many NLP datasets, including translation, question-answering, and cloze tasks. We also identify some datasets where GPT-3's few-shot learning still struggles, as well as some datasets where GPT-3 faces methodological issues related to training on large web corpora.
        {{< /details >}}    
  - Download: [1457c0d6bfcb4967418bfb8ac142f64a-Paper.pdf](https://proceedings.neurips.cc/paper_files/paper/2020/file/1457c0d6bfcb4967418bfb8ac142f64a-Paper.pdf)
- [**BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding**](https://arxiv.org/abs/1810.04805)
  - Year: 2018
  - Authors: Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova
  - Abstract: 
        {{< details "We introduce a new language representation model called BERT, which stands for Bidirectional Encoder Representations from Transformers..." >}}
            Unlike recent language representation models, BERT is designed to pre-train deep bidirectional representations from unlabeled text by jointly conditioning on both left and right context in all layers. As a result, the pre-trained BERT model can be fine-tuned with just one additional output layer to create state-of-the-art models for a wide range of tasks, such as question answering and language inference, without substantial task-specific architecture modifications. BERT is conceptually simple and empirically powerful. It obtains new state-of-the-art results on eleven natural language processing tasks, including pushing the GLUE score to 80.5% (7.7% point absolute improvement), MultiNLI accuracy to 86.7% (4.6% absolute improvement), SQuAD v1.1 question answering Test F1 to 93.2 (1.5 point absolute improvement) and SQuAD v2.0 Test F1 to 83.1 (5.1 point absolute improvement).
        {{< /details >}}    
  - DOI: [https://doi.org/10.48550/arXiv.1810.04805]()
  - Download: [1810.04805.pdf](https://arxiv.org/pdf/1810.04805.pdf)
- [**Delta Lake: High-Performance ACID Table Storage over Cloud Object Stores**](https://databricks.com/wp-content/uploads/2020/08/p975-armbrust.pdf)
  - Year: 2020
  - Authors: Michael Armbrust, Tathagata Das, Liwen Sun, Burak Yavuz, Shixiong Zhu, Mukul Murthy, Joseph Torres,Herman vanH ovell,AdrianIonescu, Alicja Łuszczak,Michał Switakowski, Michał Szafranski, Xiao Li, Takuya Ueshin, Mostafa Mokhtar, Peter Boncz1, Ali Ghodsi,Sameer Paranjpye, Pieter Senster, Reynold Xin, Matei Zaharia
  - Abstract: 
        {{< details "Cloud object stores such as Amazon S3 are some of the largest and most cost-effective storage systems on the planet, making them an attractive target to store large data warehouses and data lakes..." >}}
            Unfortunately, their implementation as key-value stores makes it dif- ficult to achieve ACID transactions and high performance: metadata operations such as listing objects are expensive, and consistency guarantees are limited. In this paper, we present Delta Lake, an open source ACID table storage layer over cloud object stores initially developed at Databricks. Delta Lake uses a transaction log that is compacted into Apache Parquet format to provide ACID properties, time travel, and significantly faster metadata operations for large tabular datasets (e.g., the ability to quickly search billions of table partitions for those relevant to a query). It also leverages this de- sign to provide high-level features such as automatic data layout optimization, upserts, caching, and audit logs. Delta Lake tables can be accessed from Apache Spark, Hive, Presto, Redshift and other systems. Delta Lake is deployed at thousands of Databricks customers that process exabytes of data per day, with the largest instances managing exabyte-scale datasets and billions of objects.
        {{< /details >}}    
  - DOI: [https://doi.org/10.14778/3415478.3415560](https://doi.org/10.14778/3415478.3415560)
  - Download: [p975-armbrust.pdf](https://databricks.com/wp-content/uploads/2020/08/p975-armbrust.pdf)