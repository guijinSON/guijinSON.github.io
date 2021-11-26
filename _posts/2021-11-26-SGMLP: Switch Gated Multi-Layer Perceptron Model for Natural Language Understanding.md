---
title: Curiosity Powered Reinforcement Learning.
layout: post
categories: [NLP, Attention, MLP]
image: assets/img/An Intrinsic Motivation for Reinforcement Learning/cover.png
description: "SGMLP"
---

Indeed, it's been a while since my last post on this blog, and to make an excuse, I have been quite busy the last few month. 
The massive busyness, however, did reward me with significant output. 
Most importantly I published my first research paper <strong>"SGMLP: Switch Gated Multi-Layer Perceptron Model for Natural Language Understanding." </strong>
Unfortunately, the paper left much to be desired for it to be called well-written. 
One significant limitation of my paper was that it was written in Korean, making it hard to be shared with non-Korean communities. 
Being so, todays post is an English review for my paper hoping that our findings can also be easily delivered to others. 

Nonetheless, despite such, I am still fairly proud that I started making novel contributions to the field and is eager to keep up my career as an A.I researcher. 

* hello
{:toc}

### Brief Introduction 

With the introduction of the Transformer [1], the Attention mechanism became the one and only architecture dominating the field of Natural Language Processing (NLP). 
Resultingly, in the status quo, the majority of NLP models adopt similar structures and suffer from analgous problems. 
Me and my research team, being inspired by the recent adoption of Multi-Layer Perceptron(MLP) in numerous fields, present a novel attention-less architecture aiming to 
add some diversity to the sphere of NLP research.  

The objectives of our model is to stage an attention-less pretrained language model showing near-BERT performances 
and prove that any scalable architecture can function as an alternative to the Attention mechanism in the field of NLP.
