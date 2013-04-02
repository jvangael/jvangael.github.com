---
layout: post
title: "Parallel Random Number Generators"
description: ""
category:
tags: [iHMM,Large Scale ML,Machine Learning]
---
{% include JB/setup %}

We recently got a paper accepted in EMNLP where we elaborate on a point that was touched upon in Mark Johnson’s [Why doesn’t EM find good HMM POS-taggers?](http://acl.ldc.upenn.edu/D/D07/D07-1031.pdf): if we are going to do completely unsupervised POS-tagging, how can non-parametric Bayesian methods help us? There were two parts to our paper: extending the iHMM to be able to handle a medium sized text corpus and an evaluation of the results to see how the iHMM states correspond to POS tags. I’ll blog about our findings later but one thing that came up during this research was the following: because of the size (1,000,000 datapoints) of the corpus (Wall Street Journal of Penn Treebank) we used, we wanted to parallelize the forward-filtering backward-sampling (FFBS) part of the inference. Because all the sentences are independent given the transition matrix and output parameters, we can easily run the FFBS in parallel.

One thing I started thinking about is the following: imagine I run on a machine with 4 cores and I start a thread for each core to process a chunk of the data. Since the FFBS is a sampling algorithm, each of these 4 threads needs to access a random number generator (RNG). I know of two ways to go about this:
* We use one RNG and access it from the 4 threads. Since the RNG’s I use are stateful, we need to lock them when we query them from a number so it’s internal state doesn’t get messed up. Locking an RNG can incur a large overhead and easily becomes the bottleneck of the parallelization.
* Use one RNG for each thread. How do we initialize them though? I use the [.NET System.Random](http://msdn.microsoft.com/en-us/library/system.random.aspx) RNG which uses a time dependent random seed. I don’t think this is a good idea because of the resolution of this time dependent seed is to coarse, and my 4 threads start almost at the same time, they might all end up using the same seed. An alternative is to initialize a global RNG to produce the seeds for the thread local RNG’s.

The second alternative in (2) is what we used but it does worry me a little bit: how can I know that the streams of random numbers in different threads are going to be ‘good enough’ (whatever that means). As a non-expert on RNG’s I’d like to know whether I’m going to get into trouble with these kinds of approaches. Matlab has a way to generate 3 statistically independent streams using the same RNG with the same seed. This seems like a step in the right direction, but it doesn’t solve my quad core problem, let alone when we run our algorithm on many more cores in Amazon Elastic Map Reduce ...

Any creative solutions out there?