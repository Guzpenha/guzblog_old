---
layout: post
title:  "Social Network Analysis"
date:   2015-08-21 12:00:00
categories: update
comments: true
---



Social Networks
==========================================================
One of the topics of my research as an undergraduate at my university database laboratory [LBD][lbd] is on [Social Network Analysis][sna], which is a field involved with the study of relations that connect people. Examples of such networks are friendships, work-relations and social-media. Studying 
these interactions and their actors is by no means recent, although modern technology has introduced new dimensions to these interactions, which can now happen in a different speed
and intensity. An introductory book aimed for undergraduate students, with a inter-disciplinary approach has been released recently and its becoming more and more influential.
It is named "Networks, crowds, and markets: Reasoning about a highly connected world" and can be read [here][kleinberg]. This book provides a really nice introduction to those who want to 
study this subject further. 

Scientific Collaboration Networks
===========================================
I have been working with a specific kind of network that is build when two researchers publish a paper togheter. 
A representation of this network can be made, where the nodes are the authors and the vertexes represent 
the coauthorship relation when publishing a paper. One great software to visualize networks in this graph notation is [Gephi][gephi], the figure above
represents the Scientific Collaboration Network of a prestigious conference here in Brazil called [SBBD][sbbd] accounting for 30 years of publications. The 
size and the color strength of the edges in this picture are proportional a weight scheme by Newman that measures the intensity of the collaboration between authors.

![SBBD Network]({{ site.baseurl }}/images/gephi.png)	

Studying these coauthorship networks might be very insightful,  for example in understanding how distinguished researchers collaborate as well as how Science evolves. 
One could also use this network to rank researchers in performance and better understand how they connect and influence others. 
This could be useful for example in the process of funding graduate programs or researchers, so much as finding the best study program to be part of.


NetworkX
===============================

Here I will just introduce this incredible python package which is helping a lot in my research, which is called
[NetworkX][networkx]. Here you can find a very wide range of alghoritms to run at graphs (SNA metrics, clustering, cliques, components, cores, distances measures, flow), a lot of implemented 
graph generators, import graphs using a lot of different formats, as well as drawing them for visualization. It has
really intuitive examples and it is simple to use. Don't waste your time implementing something that is so easily accessible, just
use NetworkX. Look at the following example of using NetworkX to calculate a SNA metric named assortativity :

{%highlight python %}
G=nx.path_graph(4)
r=nx.degree_assortativity_coefficient(G)
print("%3.1f"%r)
#-0.5
{% endhighlight%}



[lbd]: http://lbd.dcc.ufmg.br/
[sna]:https://en.wikipedia.org/wiki/Social_network_analysis#cite_note-1
[kleinberg]: http://www.cs.cornell.edu/home/kleinber/networks-book/
[gephi]: http://gephi.github.io/
[sbbd]: http://dexl.lncc.br/sbbd2015/
[networkx]: http://networkx.github.io/