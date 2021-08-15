---
title: An NLP Classic, BERT.
layout: post
categories: [Typography, Markdown, Tips]
image: assets/img/An NLP Classic, BERT/bert.png
description: "Here I go!"
---

The first paper I would be reviewing on my blog is an NLP classic, *"BERT: Pre-Training of Bidirectional Transformers for Language Understanding"*.
 It has been a while since I have first encountered this paper, but BERT is still the outset of most State-of-the-Arts(SOTA) NLP models, therefore going over this architecture will make future paper reviews way more tractable. 

* hello
{:toc}

### Brief Introduction
BERT is a powerful language encoding model, which obtained SOTA results on eleven NLP leaderboards only with minor modifications for each task.
The BERT architecture is commonly mentioned as a counterpart for the GPT, a language model from OpenAI, except the fact that it is designed to encode information "bidirectionally"(just like a Bi-LSTM) boosting its performance in sentence-level tasks.  

### General Language Representations
Just like ELMo (Peters et al .,2018), BERT is also a General Language Representation model which means, that given a sequence of input tokens the model will output a fixed-sized vector (usually Sequence Length * Hidden Dimension). In order for the model to acquire its ability to construct meaningful output representations, it undergoes a process called **Pre-Training**. This paper introduces two Pre-Training objectives, **Masked Langauge Modeling(MLM)** and **Next Sentence Prediction (NSP)**. Each objective attempts to add on different features, MLM is expected to help learn token-level relationships and knowledge, and NSP attempts to supervise BERT with sentence-level information.  

For MLM, the data generator intentionally corrupts the input by replacing 15% of the tokens at random. The final output vectors corresponding to the corrupted tokens are fed into a softmax function for the entire vocabulary, and the vocab with the highest prob is predicted as the original token (the one before corruption). This way of training, however, has been pointed out to cause a problem called, **Pretrain-Finetune Discrepancy**. Pretrain-Finetune Discrepancy refers to a mismatch caused by MLM, as no tokens are masked during downstream tasks. (Naively, the BERT model might train itself to classify only those with [MASK] tokens as a valid sentence.) To mitigate such problems, instead of replacing every 15% of the randomly selected tokens with masks, the paper adopts a mixed masking strategy.

image: assets/img/An NLP Classic, BERT/masking.png
