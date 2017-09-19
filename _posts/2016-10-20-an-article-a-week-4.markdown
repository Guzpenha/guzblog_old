---
layout: post
title:  "What's behind Amazon's Stream - An article a week #4"
date:   2016-10-20 12:00:00
categories: update
comments: true
image:
  background: triangular.png
---

## Amazon's efforts for personal recommendations
[Stream](https://www.amazon.com/stream), Amazon's new discovery page, is a visual platform for browsing and discovering new products, directed for users who have no specific intent yet. It learns user preferences and to diversify in order to recommend interesting products, increasing overall users CTR (Click Through Rate). Amazon's Personalization Sciences group is behind this project. They have published this paper at RecSys 2016 and received the Best Paper award in the short papers category.

![stream](/images/amazon_stream.png){: .center-image}

The system is divided into three components, an Item Relevance Scorer, a Submodular Diversification Framework and a Category Preference Learner. I'll briefly review them, but you can read the full article [here](http://dl.acm.org/citation.cfm?doid=2959100.2959171).

## Item Relevance Scorer
This component will generate a score for each product, by doing a Bayesian Linear Probit regression, which maps item attributes to users probability of clicking it. They've chosen to apply Thompson sampling in order to avoid a bias towards popular items of the catalog in spite of underexposed or recently added items. It will balance exploiting highly relevant items and exploring undersampled parts of the catalog. This score is global, so if this was the only part of the system then the products list would be the same for every user.

## Submodular Diversification Framework
Besides minimizing prediction errors, recommenders need to worry about the diversification of the items. When this is not taken into account, a user can receive a lot of the same things. They 've modeled this problem as a submodular optimization problem, which is a special case of the maximum set cover problem, which is NP-hard. They use an iterative greedy procedure to obtain a good enough solution to the problem of maximizing the diversity of categories of products.

## Personalization
The global category weights are learned from CTR with additive smoothing, without correction for the position of items on the screen. So they use the number of clicks and view to estimate category weights with a simple formula. On the other hand, they also learn user-specific weights, in order to personalize recommendations.  They assume that the clicks of a user are drawn from a Multinomial distribution with parameters w, that is drawn from a Dirichlet. 

## Results
They have outperformed baselines for the diversifier, the weights of each category learned adaptively from clicks and the personalized weights. The following table summarizes their improvements of CTR over these baselines.

![results_amazon_stream](/images/results_amazon_stream.png){: .center-image}




