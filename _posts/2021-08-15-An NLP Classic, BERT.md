---
title: An NLP Classic, BERT.
layout: post
categories: [NLP, BERT,Attention]
image: assets/img/An NLP Classic, BERT/bert.png
description: "An NLP Classic, BERT."
---

The first paper I would be reviewing on my blog is an NLP classic, *"BERT: Pre-Training of Bidirectional Transformers for Language Understanding"*.
 It has been a while since I have first encountered this paper, but BERT is still the outset of most State-of-the-Arts(SOTA) NLP models, so in my opinion going over this architecture will make future paper reviews way more tractable. 

* hello
{:toc}

### Brief Introduction
BERT is a powerful language encoding model, which obtained SOTA results on eleven NLP leaderboards only with minor modifications for each task.
The BERT architecture is commonly mentioned as a counterpart for the GPT, a language model from OpenAI, except the fact that it is designed to encode information "bidirectionally"(just like a Bi-LSTM) boosting its performance in sentence-level tasks.  

### General Language Representations
Just like ELMo (Peters et al .,2018), BERT is also a General Language Representation model which means, that given a sequence of input tokens the model will output a fixed-sized vector (usually Sequence Length * Hidden Dimension). In order for the model to acquire its ability to construct meaningful output representations, it undergoes a process called **Pre-Training**. This paper introduces two Pre-Training objectives, **Masked Langauge Modeling(MLM)** and **Next Sentence Prediction (NSP)**. While each objective attempts to add on different features, MLM is expected to help learn token-level relationships and knowledge, and NSP attempts to supervise BERT with sentence-level information.  

For MLM, the data generator intentionally corrupts the input by replacing 15% of the tokens with a \[MASK] token at random. The final output vectors corresponding to the corrupted tokens are fed into a softmax function for the entire vocabulary, and the vocab with the highest prob is predicted as the original token (the one before corruption). This way of training, however, has been pointed out to cause a problem called, **Pretrain-Finetune Discrepancy**. Pretrain-Finetune Discrepancy refers to a mismatch caused by MLM, as no tokens are masked during downstream tasks. (Naively, the BERT model might train itself to classify only those with \[MASK] tokens as a valid sentence.) To mitigate such problems, instead of replacing every 15% of the randomly selected tokens with masks, the paper adopts a mixed masking strategy.

<image src="https://raw.githubusercontent.com/guijinSON/guijinSON.github.io/8bfc87a2e5086ee8062b2b1c1e1f085e94574c5f/assets/img/An%20NLP%20Classic%2C%20BERT/masking.png" width=500px />   
  
As shown above, the paper examines different masking strategies and consequently, they do not replace every selected token with a mask. Instead, only 80% of the selected tokens are masked, the other 10% is replaced with a random vocabulary, and the left 10% remains unchanged.  

Since MLM fails to capture the relationship between sentences, NSP is introduced. For the NSP task, the data generator constructs the input sentence by merging two different sentences *A* and *B*. 50% of the time *B* is the actual next sentence for *A*, while for the other half they are two irrelevant sentences. By predicting whether the two sentences come from the same context, BERT is expected to learn understand sentence-level information.  

### Model Architecture 
BERT adopts an architecture very reminiscent of that of a Transformer (Vaswani et al .,2017). However, being an encoder-only model instead of inheriting the entire coupled structure it only makes use of the encoder part. A BERT_Base model would stack 12 blocks of encoders, where each is compromised of **causal self-head attentions** and a **feed-forward network**.

<image src="https://raw.githubusercontent.com/guijinSON/guijinSON.github.io/master/assets/img/An%20NLP%20Classic%2C%20BERT/architecture.png" width=200px/>

In the given structure, the causal self-head attention aims to capture the relationship between tokens, especially semantic information. On the other hand, the feed-forward network serves as a fancy concatenation layer that learns non-linear hierarchical features. One aspect that differentiates BERT from the Transformer is its input embeddings, unlike its predecessor, BERT sums token, segmentation, and positional embeddings for its input. These are intended to provide additional information to help the model encode both token and sentence level information.

<image src="https://raw.githubusercontent.com/guijinSON/guijinSON.github.io/master/assets/img/An%20NLP%20Classic%2C%20BERT/embedddings.png" width=600px /> 

### Performance & Implications  
As mentioned above BERT achieves significant results in multiple leaderboards only through minimal modifications, referred to as **Fine-Tuning**. In the Fine-Tuning process a classification head (mostly a shallow neural network) is added to the final part of the model, and by training both pre-trained parameters, and the newly initialized classification head, BERT fits itself to the given downstream task. This way of two-step training has allowed the creation of a general language model applicable for diverse tasks, and as a result, BERT performs greatly in numerous tasks as shown below.  

<image src="https://raw.githubusercontent.com/guijinSON/guijinSON.github.io/master/assets/img/An%20NLP%20Classic%2C%20BERT/benchmark.png" width=600px />   

Obviously, this piece of work from 2018 is not even close to the state of arts at the moment. BERT, however, successfully proves the significance of an encoder structure in language understanding tasks, and moreover, it shows massive scalability confirming that a bigger model would result in even more promising results.  

The paper today, BERT, is a great one to start with, and I will soon return with researches that add on. I hope you enjoyed reading. Meet me in the next post:) 



### References

\[1] [Devlin, Jacob, et al. "Bert: Pre-training of deep bidirectional transformers for language understanding." arXiv preprint arXiv:1810.04805 (2018).](https://arxiv.org/pdf/1810.04805.pdf)  
\[2] [Peters, Matthew E., et al. "Deep contextualized word representations." arXiv preprint arXiv:1802.05365 (2018).](https://arxiv.org/abs/1802.05365)  
\[3] [Vaswani, Ashish, et al. "Attention is all you need." Advances in neural information processing systems. 2017.](https://arxiv.org/abs/1706.03762)
