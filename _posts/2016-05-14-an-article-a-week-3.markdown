---
layout: post
title:  "Are recommendations always good ?- An article a week #3"
date:   2016-05-14 10:00:00
categories: update
comments: true
---

## _"To Personalize or Not: A Risk Management Perspective"_


This article studies when recommendations are actually accurate for a given user, in order to, for example, avoid making personalizations for users where the system will probably disappoint and are better to recommend the most popular items. So the idea behind is to make Recommender Systems more robust, avoiding failing drastically for some users.

	@inproceedings{zhang2013personalize,
	  title={To personalize or not: a risk management perspective},
	  author={Zhang, Weinan and Wang, Jun and Chen, Bowei and Zhao, Xiaoxue},
	  booktitle={Proceedings of the 7th ACM Conference on Recommender Systems},
	  pages={229--236},
	  year={2013},
	  organization={ACM}
	}


This concept was recently introduced to Information Retrieval area, where models need to cope with risk and to improve robustness. In IR we could think of this in terms of tradeoff between robustness (minimizing the probability of significant failure relative to a provided baseline) and effectiveness (overall gains across queries). It is possible to borrow the same concepts to Recommender Systems, where queries are now users, and we want to increase overall effectiveness over users but we do not want to fail (compared to a provided baseline) any user. So the idea is to propose new models that, besides outperforming the previous model, do not lose to a baseline in any user (how bad would it be if a new model makes it better for some users but for you it makes all your recommendations trash). Check below a comparision of a popularity baseline and a Bayesian personalized ranking(BPR).

![pop_bpr]({{ site.baseurl }}/images/pop_bpr.png){: .center-image}

The authors of this article presents basic concepts of [portfolio retrieval](http://web4.cs.ucl.ac.uk/staff/jun.wang/papers/2009-sigir09-portfoliotheory.pdf) which quantifies documents on the basis of its expected overall relevance and variance,inspired by an economic theory dealing with investment in financial markets. They bring such concepts to Recommender Systems area in order to propose a switch algorithm that makes decisions between personalized and non-personalized recommendation. Besides that, they use a Bayesian latent factor model to estimate the user expected reward and variance and along with item portfolio optimization used to propose a re-ranking approach.

![reranking]({{ site.baseurl }}/images/reranking.png ){: .center-image  }

The principle is to understand how well the recommender system has captured the user personal interest , by mean-variance-aware analysis, in order to decide if it is best to personalize or not. In other words, which of the portifolios dominates(the personalized or the non-personalized) the other. They discovered that diversifying a ranking list reduces the risk of a recommended item list. The experiments on both netflix and movielens dataset showed the effectiveness of the reranking and switch algorithms. 

![switch_perf]({{ site.baseurl }}/images/switch_performance.png){: .center-image}


I personally think that reserachers should take into account, besides statistical significance tests, also a risk-sensitive evaluation when comparing two competing recommender system models. This makes it even harder to propose models that present a overall gain in effectiveness but won't make all users recommendations better.
