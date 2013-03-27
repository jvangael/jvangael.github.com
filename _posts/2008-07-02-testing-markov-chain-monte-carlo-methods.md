---
layout: post
title: "Testing Markov Chain Monte Carlo Methods"
description: ""
category:
tags: [Machine Learning]
---
{% include JB/setup %}

The projects I was involved in this year all used Markov Chain Monte Carlo (MCMC) methods for inference. MCMC methods are nice because they are so widely applicable. However, I often find them much harder to debug than variational methods. When coding up a new MCMC algorithm I use the following "procedure" to debug my code:
* Fix parameters in the model and generate a lot of data. Initialise the sampler with all hidden variables set to the values used to generate the data. Run the sampler and check that it doesn't move too much. It is crucial to generate a lot of data so there is little uncertainty in the parameters and there is little reason for the sampler to move around. This test is really to check that if the inference algorithm is working, it should recognize that it has found a solution.
* Fix parameters in the model and generate a lot of data. Initialise the sampler with random hidden variables. Run the sampler and check that it discovers the parameters you used to generate the data. Again, this would work if there is enough data so there is little uncertainty in the posterior distribution of the parameters. This test is to check the search abilities of the inference algorithm.
* Finally, I apply the model and algorithm to real data. At this point, I will probably dig up [Bayesian Data Analysis](http://books.google.com/books?id=TNYhnkXQSjAC) and use more principled ways to assess convergence.

In variational methods one can check that a lower bound increases between iterations; if it doesn't, something is wrong. Are there similar kind of checks for sampling algorithms? Do people have some good suggestions for debugging MCMC methods?
