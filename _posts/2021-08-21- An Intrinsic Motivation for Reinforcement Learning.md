---
title: An Intrinsic Motivation for Reinforcement Learning.
layout: post
categories: [RL,Sparse Reward,Long Term Dependency]
image: assets/img/An Intrinsic Motivation for Reinforcement Learning/cover.png
description: "An Intrinsic Motivation for Reinforcement Learning."
---

For the moment, I am working at a firm called QRAFT, and over here everyone is a huge fan of Reinforcement Learning (RL). It is quite awkward to be the only NLP guy onboard, but one thing great about it is that I get to learn a lot about RL, which I originally knew nothing about. Last week I was going over some RL papers that deal with Long Term Dependency problems, an issue also very prevalent in the NLP domain, and this one named **_"Curiosity-driven Exploration by Self-supervised Prediction"_** just struck me in the head.

* hello
{:toc}

### Brief Introduction 

Reinforcement Learning usually refers to a structure comprised of an agent and an environment. The agent learns to make actions adequate to its given state through experience and exploration and converges towards a structure that maximizes its cumulative reward. Accordingly, rewards are a very important indicator that guides the agent, however, in most real-life problems extrinsic rewards are extremely sparse (or extremely far away) making it difficult to construct a shaped reward function. This paper proposes a concept called **_curiosity_**, which generates continuous intrinsic rewards to ameliorate such issues and succeeds to outperform past papers in reward-sparse environments.  

### Intrinsic Curiosity Model 

Unlike most Online-RL, this paper adopts an additional structure named **_Intrinsic Curiosity Model(ICM)_** that generates intrinsic rewards for the agent. Along with the concept of curiosity, the paper also argues that it is inefficient for the model to make predictions in the raw sensory space (e.g. pixels), and suggests that the environment should be projected into a feature space for a better prediction. Therefore, the ICM is made up of two subsystems; the **inverse dynamics model** and the **forward model**.


### Reference

\[1] [Pathak, Deepak, et al. "Curiosity-driven exploration by self-supervised prediction." International conference on machine learning. PMLR, 2017.](https://arxiv.org/abs/1705.05363) 
\[2] 
