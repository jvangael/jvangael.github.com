---
layout: post
title: "If pigs can whistle, horses can fly."
description: ""
category:
tags: [Statistics]
---
{% include JB/setup %}

We talked about the concept of exchangeability [a few weeks ago](). I presented three urn models, two of which defined exchangeable probability distributions. The main idea I wanted to convey using the first and second urn models was that exchangeability is not just independence: urn model 2 does not look exchangeable at first sight but some simple algebra convinced us that it is.

Today I want to continue this discussion with a theorem that is strongly related to exchangeability called _de Finetti's_ theorem. The theorem goes as follows: say we have an infinite sequence of binary random variables $x_1, \cdots, x_n$ (say the color of the balls in our urn model) and this sequence is exchangeably, then there exists a parametric model $p(x|\theta)$ and prior $p(\theta)$ such that
$$p(x_1, \cdots, x_n) = \int_\theta \prod_{i=1}^n p(x_i|\theta) p(\theta) d\theta$$

In other words, if our sequence of random variables is exchangeable, than it really is a sample from a mixture model.

This kind of theorem reminds me of a quote I once heard in a complexity theory talk: if pigs can whistle, then horses can fly. What do I mean by this? Assuming that a set of random variables is exchangeably doesn't sounds like a very big assumption: e.g. if you plan to cluster something like the MNIST digit recognition dataset, there is nothing a priori that distinguishes one image from another; aka. you could assume they are exchangeable. However, once you make the exchangeability assumption, De Finetti's theoremy suddenly says that really your datapoints are part of a hierarchicaly Bayesian model. In other words: by making the relatively innocent exchangeability assumption, De Finetti's theorem imposes the graphical model structure upon you. A weak assumption implies a rather strong consequence.

There is a catch however: the theorem does not specify what kind of random variable $\theta$ is, nor what its density $p(\theta)$ is. As a matter of fact, $\theta$ could be a random variable over an infinite dimensional space (which would lead us into the realm of nonparametric Bayesian models such as the Dirichlet Process, but that's for another time). For simple models such as urn model 2 we can compute the distribution though: $\theta$ turns out to be a Beta distributed random variable.

All in all, De Finetti's theorem is an interesting theorem but it is not clear to me of how much practical value it is. There are many extensions and modifications of the theorem; for more information check
* [The Concept of Exchangeability - Jose Bernardo](http://www.uv.es/~bernardo/Exchangeability.pdf)
* [Exchangeability and Related Topics - David Aldous](http://www.stat.berkeley.edu/~aldous/Papers/me22.pdf)