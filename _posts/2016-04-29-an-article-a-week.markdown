---
layout: post
title:  "Automatically Learning Programs"
date:   2016-04-30 12:00:00
categories: update
comments: true
published: false
---

## A Computer Science article a week, the series begins 




This is the start of a new series in my blog where I try to make a commentary about a computer science article per week.
I will be selecting articles out of my interest, so expect the following areas to be featured here: recommender systems, machine learning, deep learning, social networks, data mining and information retrieval.

![begins]({{ site.baseurl }}/images/batman.gif){: .center-image } 


## The first article (Neural Programmer-Interpreters, 2015)


The article I choose is __Neural Programmer-Interpreters__ by Scott Reed and Nando de freitas from Google DeepMind, it can be read [here](http://arxiv.org/abs/1511.06279){:target="_blank"}. For the interested in the bibtex, here it goes:


```
@article{reed2015neural,
  title={Neural Programmer-Interpreters},
  author={Reed, Scott and de Freitas, Nando},
  journal={arXiv preprint arXiv:1511.06279},
  year={2015}
}
```

The problem tackled by this article is learning to __represent and execute problems automatically__, which is closely related to program induction, i.e. inducing a program given example input and ouput pairs. They propose a recurrent and compositional neural network in order to do that. In their experiments,  NPI (Neural Programmer-Interpreter) architecture learns 21 programs, claiming at the same time a higher generalization power then other [LSTMs](https://en.wikipedia.org/wiki/Long_short-term_memory){:target="_blank"}. Other works follow this idea in the literature, however _reed2015neural_ differ by incorporating compositional structure into the network using program memory. This means that the model can learn new programs by combining sub-programs.


The tasks used in the _Experiments_ section are: __addition__ (the model should learn how to do the standard grade school alghoritm), __sorting__ (the model should learn how to sort an array of numbers using [bubblesort](https://en.wikipedia.org/wiki/Bubble_sort){:target="_blank"}) and __canonicalizing 3D car models__ (see figure below from the article).

![car]({{ site.baseurl }}/images/car_canonicalization.png){: .center-image}


I will not describe how the model trains or makes inferences, but the results show it to be more accurate in some tasks, as well as able to generalize better (i.e: accuracy can remain 100% while sorting sequences up to a length of 60). I have the impression that, even though the problem in question is an extremely interesting and awesome task, the problems learnt by this recurrenct and compositional neural network are still simple programs, and fail to be accurate on small sizes of input (60 numbers for example in sorting). 

![accuracy_generalization]({{ site.baseurl }}/images/npi_accuracy.png){: .center-image}

Nonetheless, the article is really interesting, besides acomplishing what I summarized before, NPI can be trained with a fixed core and it is able to learn new programs without forgetting already learned program and it is modeled in a way that the aim is to provide fewer labeled examples, but where they contain richer information so that the model can learn compositional structure. 

This is a step towards achieving real artificial intelligence, which our current machine learning is still very far. Further reading in the subject the article comprises:

* [Inferring Algorithmic Patterns with Stack-Augmented Recurrent Nets](http://arxiv.org/abs/1503.01007){:target="_blank"}
* [Learning Simple Algorithms from Examples](http://arxiv.org/abs/1511.07275){:target="_blank"}
* [Neural Programmer: Inducing Latent Programs with Gradient Descent](http://arxiv.org/abs/1511.04834){:target="_blank"}

![car]({{ site.baseurl }}/images/exmachina.gif){: .center-image}
