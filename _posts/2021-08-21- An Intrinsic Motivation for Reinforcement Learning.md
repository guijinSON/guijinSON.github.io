---
title: Curiosity Powered Reinforcement Learning.
layout: post
categories: [RL,Sparse Reward,Long Term Dependency]
image: assets/img/An Intrinsic Motivation for Reinforcement Learning/cover.png
description: "Curiosity Powered Reinforcement Learning."
---

For the moment, I am working at a firm called QRAFT, and over here everyone is a huge fan of Reinforcement Learning (RL). It is quite awkward to be the only NLP guy onboard, but one thing great about it is that I get to learn a lot about RL, which I originally knew nothing about. Last week I was going over some RL papers that deal with Long Term Dependency problems, an issue also very prevalent in the NLP domain, and this one named **_"Curiosity-driven Exploration by Self-supervised Prediction"_** just struck me in the head.

* hello
{:toc}

### Brief Introduction 

Reinforcement Learning usually refers to a structure comprised of an agent and an environment. The agent learns to make actions adequate to its given state through experience and exploration and converges towards a structure that maximizes its cumulative reward. Accordingly, rewards are a very important indicator that guides the agent, however, in most real-life problems extrinsic rewards are extremely sparse (or extremely far away) making it difficult to construct a shaped reward function. This paper proposes a concept called **_curiosity_**, which generates continuous intrinsic rewards to ameliorate such issues and succeeds to outperform past papers in reward-sparse environments.  

### Intrinsic Curiosity Model 

Unlike most Online-RL, this paper adopts an additional structure named **_Intrinsic Curiosity Model(ICM)_** that generates intrinsic rewards for the agent. Along with the concept of curiosity, the paper also argues that it is inefficient for the model to make predictions in the raw sensory space (e.g. pixels), and suggests that the environment should be projected into a feature space for a better prediction. Therefore, the ICM is made up of two subsystems; the **inverse dynamics model** and the **forward model**.

<image src="https://raw.githubusercontent.com/guijinSON/guijinSON.github.io/master/assets/img/An%20Intrinsic%20Motivation%20for%20Reinforcement%20Learning/icm.png" width=500px />  

When the ICM is given states \\(S_t \\) and \\(S_{t+1} \\) as input it encodes them to vectors on the feature space; \\(\phi({S_t}) \\) and \\(\phi({S_{t+1}}) \\). Once the projection is done, the inverse dynamics model use these values to predict \\(\hat{a_t} \\), the action at sequence \\(t \\). By measuring the discrepancy between actual and predicted actions the neural network learns to predict. better future actions.

In the meantime, the forward model receives \\(a_t \\) and \\(\phi({S_t}) \\) to predict \\(\hat\phi(S_{t+1}) \\). This prediction error represents the agent's knowledge about the environment it lies in, and function as intrinsic reward, signaling the agent its lack of understanding and need for additional training.

### Prediction Error as Curiosity  

As mentioned above, previous RL agents barely showed meaningful performance in sparse-reward environments. To mitigate such issue, this paper trains its neural net to maximize the sum of both extrinsic and intrinsic rewards \\(r_t = r^i_t + r^e_t\\). The intrinsic reward  \\(r^i_t \\), is the prediction error generated from the forward model and supplements the \\(r^e_t \\) which is mostly zero. By using the prediction error from the feature space (instead or the raw sensory space) the paper attempts to only encode environmental features important for the agent. The paper identifies three cases of environment observation.

1. Things that can be controlled by the agent  
2. Things that the agent cannot control but that can affect the agent   
3. Things out of agent's control and not affecting the agent 

Since an agent does not have an incentive to learn about insignificant variations, the paper assumes that the projection layer will eventually learn to only encode information from cases \[1] and \[2]. Resultingly, the model acquires an encoder robust towards distractor objects and other nuisance sources of alterations allowing the model to easily generalize to noisy or unseen scenarios. In a nutshell, the forward model from the ICM not only provides continuous rewards that fuel the model but it also enhances the robustness of the agent as a whole. 

### Performance

The paper tests the model in diverse settings proving its \[1] Strength in sparse-reward environments, \[2] Robustness towards noisy input and [3] the ability to generalize to novel scenarios. 

First up, the paper compares **ICM+A3C**, **ICM(pixel) + A3C** and a **vanilla A3C** model in dense, sparse and very sparse reward settings. The ICM(pixel) resembles a normal ICM except the fact that it uses features from the raw sensory space instead of projecting it to a separate latent area. As the figure below indicates, the ICM option greatly vanquishes the other as the reward gets sparser, implying that its way of signaling the model through prediction error supervises the agent in a correct direction.   

<image src = "https://raw.githubusercontent.com/guijinSON/guijinSON.github.io/master/assets/img/An%20Intrinsic%20Motivation%20for%20Reinforcement%20Learning/reward.png" width=850px />  

Second, the authors test the model in a **Viz-Doom 3-D navigation** task but only after augmenting it with white noise that makes up 40% of the image. Even in this setting the ICM succeeds to head towards the reward affirming strong resilience against noisy environments.     

<image src="https://raw.githubusercontent.com/guijinSON/guijinSON.github.io/master/assets/img/An%20Intrinsic%20Motivation%20for%20Reinforcement%20Learning/noisy.png" width=500px /> 

Finally, by deploying the ICM+A3C model in a novel environment the paper confirms its ability to generalize towards unseen scenarios. In the given environment, both finetuned and non-finetuned ICM model excels in learning a generalizable exploration policy, contrary to ICM(pixel) that totally fails to do so.  

<image src="https://raw.githubusercontent.com/guijinSON/guijinSON.github.io/master/assets/img/An%20Intrinsic%20Motivation%20for%20Reinforcement%20Learning/novel.png" width=500px />  

### Implications

Though it is not a totally new concept to introduce an alternative reward that the agent can utilize, this paper is significant in that the way it shapes its reward is not domain-specific. Compared to recent NLP researches that aim to solve its Long-Term Dependency problem through augmenting memorization abilities (which again encounters computing issues), this Curiosity approach seems to be way more generalizable.  
I really appreciated this random opportunity given by my coworkers that allowed me to explore subjects I have never did before and hope you also enjoyed reading my work. Thank you and meet me in the next post:)


### Reference

\[1] [Pathak, Deepak, et al. "Curiosity-driven exploration by self-supervised prediction." International conference on machine learning. PMLR, 2017.](https://arxiv.org/abs/1705.05363)  
