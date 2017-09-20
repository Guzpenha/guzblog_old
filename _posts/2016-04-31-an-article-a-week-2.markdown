---
layout: post
title:  "A probablistic social recommender system - An article a week #2"
date:   2016-04-31 12:00:00
categories: update
comments: true
---

## _"A probabilistic model for using social networks in personalized item recommendation"_

This article is related to a topic I've
studied: considering users social network to enhance the results of recommender systems.
It is the intersection of two areas in computer science: [social networks analysis](https://en.wikipedia.org/wiki/Social_network_analysis) and [recommender systems](https://en.wikipedia.org/wiki/Recommender_system). 

	@inproceedings{chaney2015probabilistic,
	  title={A probabilistic model for using social networks in personalized item recommendation},
	  author={Chaney, Allison JB and Blei, David M and Eliassi-Rad, Tina},
	  booktitle={Proceedings of the 9th ACM Conference on Recommender Systems},
	  pages={43--50},
	  year={2015},
	  organization={ACM}
	}

The idea behind is to extract additional information from friends (or people that you trust) in order personalize even more the system. There are two phenomenon studied in SNA which are important to this matter: homophily (people tend to connect with similar people) and social influence (people may modify their behaviour to align with the behaviour of their friends). Both are formalized in Chapter 4: NETWORKS IN THEIR SURROUNDING CONTEXTS from _"Networks, Crowds, and Markets: Reasoning About a Highly Connected World, David Easley and Jon Kleinberg"_.

![SNA_RS]({{ site.baseurl }}/images/sna_rs.png){: .center-image}

He builds the social factor on top of another model called Poisson Factorization (PF) which is a variant of the popular matrix factorization method for recommendation. It is assumed that the number of stars a person gives to an item is sampled from a Poisson distribution, where (similarly to matrix factorization) the rate is a a linear combination of user preference vector and item attributes. The model proposed by the article , Social Poisson Factorization (SPF), adds another component to the Poisson which captures how influenced a person is by each of his friends.  


![SPF]({{ site.baseurl }}/images/SPF.png){: .center-image}


They outperformed all other methods in six different datasets, using the NCRR metric. What I did not like is that they reported only the means, without any confidence interval or statistical test. Nonetheless this article is an interesting comparision of methods and it uses social information in a novel probabilistic model.

![SPF]({{ site.baseurl }}/images/results_spf.png){: .center-image}