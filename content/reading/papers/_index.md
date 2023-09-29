---
title: "Reading - Papers"
date: 2023-6-12T03:24:32-07:00
draft: false
layout: "single"
---

- [**Comparing deep neural networks against humans: object recognition when the signal gets weaker**](https://arxiv.org/abs/1706.06969)
  - Year: 2017
  - Authors: Robert Geirhos, David H. J. Janssen, Heiko H. Schütt, Jonas Rauber, Matthias Bethge, Felix A. Wichmann
  - Abstract: 
        {{< details "Human visual object recognition is typically rapid and seemingly effortless, as well as largely independent of viewpoint and object orientation..." >}}
            Until very recently, animate visual systems were the only ones capable of this remarkable computational feat. This has changed with the rise of a class of computer vision algorithms called deep neural networks (DNNs) that achieve human-level classification performance on object recognition tasks. Furthermore, a growing number of studies report similarities in the way DNNs and the human visual system process objects, suggesting that current DNNs may be good models of human visual object recognition. Yet there clearly exist important architectural and processing differences between state-of-the-art DNNs and the primate visual system. The potential behavioural consequences of these differences are not well understood. We aim to address this issue by comparing human and DNN generalisation abilities towards image degradations. We find the human visual system to be more robust to image manipulations like contrast reduction, additive noise or novel eidolon-distortions. In addition, we find progressively diverging classification error-patterns between humans and DNNs when the signal gets weaker, indicating that there may still be marked differences in the way humans and current DNNs perform visual object recognition. We envision that our findings as well as our carefully measured and freely available behavioural datasets provide a new useful benchmark for the computer vision community to improve the robustness of DNNs and a motivation for neuroscientists to search for mechanisms in the brain that could facilitate this robustness.
        {{< /details >}}    
  - Download: [1706.06969.pdf](https://arxiv.org/pdf/1706.06969.pdf)
- [**Attention Is All You Need**](https://arxiv.org/abs/1706.03762) (aka the very influential and important 'The Transformer Paper')
  - Year: 2017
  - Authors: Robert Geirhos, David H. J. Janssen, Heiko H. Schütt, Jonas Rauber, Matthias Bethge, Felix A. Wichmann
  - Abstract: 
        {{< details "The dominant sequence transduction models are based on complex recurrent or convolutional neural networks in an encoder-decoder configuration..." >}}
            The best performing models also connect the encoder and decoder through an attention mechanism. We propose a new simple network architecture, the Transformer, based solely on attention mechanisms, dispensing with recurrence and convolutions entirely. Experiments on two machine translation tasks show these models to be superior in quality while being more parallelizable and requiring significantly less time to train. Our model achieves 28.4 BLEU on the WMT 2014 English-to-German translation task, improving over the existing best results, including ensembles by over 2 BLEU. On the WMT 2014 English-to-French translation task, our model establishes a new single-model state-of-the-art BLEU score of 41.8 after training for 3.5 days on eight GPUs, a small fraction of the training costs of the best models from the literature. We show that the Transformer generalizes well to other tasks by applying it successfully to English constituency parsing both with large and limited training data.
        {{< /details >}}    
  - Download: [1706.03762.pdf](https://arxiv.org/pdf/1706.03762.pdf)