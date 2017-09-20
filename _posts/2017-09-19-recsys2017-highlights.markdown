---
layout: post
title:  "RecSys 2017 Highlights"
date:   2017-09-19 10:00:00
categories: update
comments: true
image:
  feature: como.jpg
---

<!-- ![alt](/images/image.png){: .center-image}  -->

In this post I will give my personal thoughts on some articles from 2017 ACM Conference on Recommender Systems, that I chose out of my own interest, with no specific order, divided by recent trends in the area. If you believe I misunderstood any of the papers please correct me. The main topics covered are:

- Explanations and Model Interpretability
- Deep Learning and Session-Based RS
- Gap between academia and industry

# Explanations and Model Interpretability

**[User Preferences for Hybrid Explanations](http://dl.acm.org/citation.cfm?id=3109859.3109915):** Authors compare different types of explanations - obtained from different sources in a hybrid recommender such as contextual, social, item-based or user-based - and different visualizations - natural language, rule-based and graphical visualizations such as Venn diagrams - in order to understand which presentation styles improve users experience. Their results show that  Venn diagrams outperforms other types of explanations, but are hard to expand for three or more sources of information. Other dimensions did not show a statistically significant difference for user experience in their experiments.

<!-- ![alt](/images/recsys2017/1.png){: .center-image} -->


**[Using Explainability for Constrained Matrix Factorization](http://dl.acm.org/citation.cfm?id=3109913):** Adbollahi proposes a Matrix Factorization model that has explainability constraints, meaning that it is able to generate accurate predictions while still being able to make explanations using no additional data source (only the rating matrix). This is obtained by regularizing the loss function with the addition of a term that represents how explainable predictions are (amount of user-based neighbors or item-based neighbors). Experiments show that EMF (Explainable-Matrix Factorization) is able to generate more explainable recommendations while maintaining the accuracy of MF.

<!-- ![alt](/images/recsys2017/2.png){: .center-image} -->

**[Folding: Why Good Models Sometimes Make Spurious Recommendations](http://dl.acm.org/citation.cfm?id=3109911):** This paper is a really interesting read, it studies why sometimes matrix factorization methods make really bad recommendations in top-K results. It introduces a new metric to measure the effect of folding, which authors claim to be a major contributing factor to such spurious recommendations. Authors define folding as the phenomenon in which disparate groups are collapsed onto the same region in the embedding space. For example, users who are children having projections in embedding space (from matrix factorization ) really close to horror films, even though there is no data supporting such closeness. 

<!-- ![alt](/images/recsys2017/3.png){: .center-image} -->

Xin et. al also argue that folding happens when the model assigns high affinity to unrelated missing data. This is related to the fact that a model has to be able to discern why a user-item-rating is missing from the observations. The Missing Not At Random (MNAR) says that not all missing data have an equal likelihood of being unobserved (there is a set of items that some users will most likely never consume, and another set of items that users might eventually consume). Considering that the density of ratings in datasets is really small, the MNAR principle has to be taken into account to avoid such spurious recommendations.

**[Evaluating Decision-Aware Recommender Systems](http://dl.acm.org/citation.cfm?id=3109888):** This paper explores recommender systems that decide whether they should make a recommendation or not, based on their confidence of their recommendations. They propose two ways of measuring such confidence: support (number of neighbors that participated in the computation) in the case of nearest-neighbors algorithms and uncertainty (sd of the predictions) in the case of Probabilistic Matrix Factorization.  Experimental results show that their proposed decision-aware recommenders improve accuracy at the expense of item and user coverage. This is another step into better understanding recommender systems errors and assumptions when making spurious recommendations.

# Deep Learning and Session-Based RS

First I will talk about DLRS, which is the second workshop on DL (Deep Learning) for recommender systems, and then I will dive into some papers regarding session-based recommenders.  The first set of [slides](https://www.slideshare.net/balazshidasi/deep-learning-in-recommender-systems-recsys-summer-school-2017) from @balazshidasi  is an introduction to deep learning, explaining what it is/is not able to do,  and why it is receiving so much attention now. The main contributing factors to its success can be divided into three factors: computational power (GPU), more data and research breakthroughs.

Even though deep learning has had impressive results recently, it is not the answer to every problem in machine learning as it has its limitations. So how could we use such concepts in recommender systems? Balázs argues that DL has a potential for feature extraction directly from content (from images or text for example), modeling dynamic behavior with RNNs and generating more accurate representations of users and items.

He points [here](http://dl.acm.org/citation.cfm?id=3109953&CFID=809538421&CFTOKEN=66805074) to the state of the art when using neural networks in recommender systems: embeddings & 2vec models, extracting features from different data domains, deep models for collaborative filtering, autoencoders for collaborative filtering and session-based recommendations with RNNs. Exploring different approaches and architectures of deep models in the context of recommender systems is a promising research area.

**[Personalizing Session-based Recommendations with Hierarchical Recurrent Neural Networks](http://dl.acm.org/citation.cfm?id=3109896):**Authors in this paper extend related work by adding an extra component on RNN Session-based Recommenders that captures users profiles and information between sessions. The idea is to use a hierarchical architecture that model cross-sessions iterations by adding another RNN between user sessions, which is capable of capturing the evolution of the user across sessions and providing personalization capabilities. Their results show that the proposed approach is better than baselines and state-of-the-art RNNs that are not sensitive to cross sessions interactions and the ones where user sessions are concatenated. 

![alt](/images/recsys2017/4.png){: .center-image}

**[Modeling User Session and Intent with an Attention-based Encoder-Decoder Architecture](https://doi.org/10.1145/3109859.3109917):** Loyola et al proposed an encoder-decoder architecture for the problem of predicting which item will be seen next for a user during a session and whether he has the intention to purchase an item or not. Inspired by recent encoder-decoder approaches in machine translation, the proposed model that is a bidirectional RNN as the encoder and a normal RNN as the decoder, and authors added alignment (passing labels as well as predictions to the next time state) and attention (encapsulating expressive portions of the source sequence in a separate block) mechanisms as well.

![alt](/images/recsys2017/5.png){: .center-image}

**[When Recurrent Neural Networks meet the Neighborhood for Session-Based Recommendation](https://doi.org/10.1145/3109859.3109872):** This paper makes shows how the state-of-the-art is still not well defined for session-based recommenders. Authors point for example that GRU4REC was evaluated on a proprietary protocol, making it hard to reproduce its results. They compare the proposed heuristic-based algorithm, that uses the most similar sessions to provide recommendations using a similarity measure to predict next items on the session, with GRU4REC and a hybrid of both. Jannach et al found that the nearest-neighbor scheme performed better in multiple datasets, and the hybridization of both recommenders could improve results, even more, capturing both co-occurrence and sequential signals in the data.

# Gap between academia and industry

**[Rethinking Collaborative Filtering: A Practical Perspective on State-of-the-art Research Based on Real World Insights](http://dl.acm.org/citation.cfm?doid=3109859.3109919):** Koenigstein refers to his previous paper "The list recommendation problem", where a more appropriate task - which better relates to real-world recommenders goal - is proposed, the list recommendation problem: given a specific user u, the goal is to produce an ordered personalized list l of K items that maximize the probability that u will click on an item from l. He argues that using such formulation, there is no trade-off between accuracy and diversity, as the model will automatically learn the right amount of diversity needed.

Another point that he makes is that the trade-off between accuracy and novelty is a product of traditional CF models trying to predict the next item the user will buy, instead of optimizing for the real goal of most real-world systems, which is to influence the user to consume more items. As CF models output consists of many popular items that users would most likely consume regardless of the recommendations, current systems are failing to actually influence users behavior. He argues that a combination of CF models (which are great at learning tastes by learning embeddings of tastes) and Reinforcement Learning - which optimizes a reward function based on interactions with the system - will be the future of recommender systems.

Finally, he talks about the problem of evaluating RS, which in an offline setup has evolved from RMSE to other formulations such as rankings is very different from online experiments which are expensive and time-consuming (and sometimes impossible in academic research). This is definitively an open research area, and Koenigstein points to promising research "Learning from logged implicit exploration data" trying to mitigate this problem.

**[Déjà Vu: The Importance of Time and Causality in Recommender Systems](http://dl.acm.org/citation.cfm?doid=3109859.3109922):** This was a talk given by @JustinBasilico on how important time is for recommenders at Netflix. He stresses that handling time in offline academic experiments is different from production systems such as Netflix. From slides we can see that Basilico explores the importance of time in various contexts: during data collection and evaluation procedures, recommender algorithms that use time in their model, models learning, and recommender systems that change over time (UX, recommender algorithms, feedback loops), and during the interaction with the system, so users need less time to find something great to watch.

This is a nice reminder that evaluation procedures and methodology in academia should take into account time, for example splitting data for training models and testing them using a fixed date cut instead of user-wise.
