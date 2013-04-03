---
layout: post
title: "May All Your Wishes Come True"
description: ""
category:
tags: [Machine Learning]
---
{% include JB/setup %}

I am trying to catch up with a stack of 109 papers which are on my “To Read” list. Today I read a very enjoyable paper called [May all your wishes come true: A study of wishes and how to recognize them](http://pages.cs.wisc.edu/~andrzeje/publications/naacl-2009.pdf) by some of my former UW-Madison friends and colleagues Andrew B. Goldberg, Nathanael Fillmore, David Andrzejewski, Zhiting Xu, Bryan Gibson and Xiaojin Zhu.

The story is as follows: in 2007, the Times Square Alliance asked people to send their wished to a [Virtual Wishing Wall](http://www.timessquarenyc.org/nye/nye_interactive.html) website with the promise to print these wishes on confetti and drop it from the sky at midnight December 31, 2007. The UW-Madison people got a hold of this corpus of wishes and did some statistical analysis.
A few highlights:
* wishes follow Zipf’s law
* topic wise, US people wish more for religion
* topic wise, non-US people wish more for love, peace and travel
* scope wise, US people wish to their country and family more frequently
* scope wise, non-US people wish to the world more frequently

After the statistical analysis, the authors wanted to come up with a classifier that could detect wishes. Their approach consists of extracting wish templates in an unsupervised fashion. The idea is quite clever (and I believe more widely applicable): people often wished for “world peace” and “I wish for world peace”, or “health and happiness” and “I wish for health and happiness”. In other words, there is quite a bit of redundancy in how the wish is expressed. By matching similar wishes, the authors extract the “redundant” part and assume it is a template.

Matching wishes can be done as follows: you create a bipartite graph and loop over all wishes, if a wish contains another wish (“I wish for world peace” contains “world peace”), you create a content node on the left with the content part (e.g. “world peace”), a template part on the right with the redundancy (e.g. “I wish for”) and you connect these with a directed edge from the content to template node. When you’re done you loop over all template nodes and see whether any of them contain content words. If so, you introduce an edge from the template node to the content node. Finally, you score template nodes by their indegree – outdegree. I will refer you to table 4 to see that the results by this relatively simple algorithm are quite good.

The reason I believe this is more widely applicable is that we can imagine using this technique for extracting templates from web queries. People often query for facts: e.g. kids of Michael Jackson. Using the algorithm from this paper, we might be able to extract the most common templates which in turn would give us a good indication of what kind of answers search engines should be trying to answer. Just an idea ...
