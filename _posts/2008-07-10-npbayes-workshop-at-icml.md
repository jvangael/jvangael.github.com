---
layout: post
title: "NPBayes workshop at ICML"
description: ""
category:
tags: [Machine Learning,Conference Reports]
---
{% include JB/setup %}

Yesterday, between ICML and UAI there was the [nonparametric Bayes (NPBayes) workshop](http://npbayes.wikidot.com/) organized by [Yee Whye Teh](http://www.gatsby.ucl.ac.uk/~ywteh), [Romain Thibaux](http://www.eecs.berkeley.edu/~thibaux), [Athanasios Kottas](http://www.soe.ucsc.edu/~thanos/), [Zoubin Ghahramani](http://learning.eng.cam.ac.uk/zoubin) &amp; [Michael Jordan](http://www.eecs.berkeley.edu/~jordan). The program was packed with a lot of very interesting talks which for your convenience were recorded and will be put online at videolectures.net soon.

Just after lunch, there was a panel discussion on software for NPBayes.  I thought much of the discussion also applied to graphical models in general. The main contenders for general software are (with main pros and cons):
* the [Hierarchical Bayes Compiler](http://www.cs.utah.edu/~hal/HBC/) by [fellow blogger](http://nlpers.blogspot.com/) Hal Daume III. Pros: software is freely available, continuing development, quite a large feature set (including NPBayes components) and a group of active users to show that it actually works. Cons: the language itself is more limited than some of its contenders.
* [Church](http://www.mit.edu/~ndg/papers/churchUAI08_rev2.pdf) by Noah Goodman, Vikash Mansighka, Dan Roy, Keith Bonawitz &amp; Josh Tenenbaum. Pros: very flexible language. Cons: no software available yet.
* A proposal by Max Welling: Max and one of his students are working on a library for fast inference and are planning to add a graphical UI to design graphical models visually.
* [Infer.NET](http://research.microsoft.com/mlp/ml/Infer/Infer.htm) by Microsoft Research Cambridge. Pros: integrates with many programming languages through .NET, a great variety of inference algorithms. Cons: no free software available yet (a release is scheduled for later this year).

The workshop ended with a panel discussion on the future and prospects of NPBayes. Here are some of the questions and answers I can remember of the top of my head
* David Sontag: we've seen many Markov chain algorithms and some mean field for NPBayes. What are the prospects of using different inference algorithms? More specifically, the marginal polytope has taught us that belief propagation, Kikuchi approximations, etc ... give us approximations that have a different flavour than mean field methods. Answers:
** I think everyone agreed that there is a lot of room to explore these algorithms.
* Myself: how should we position infinite capacity models compared to finite capacity models: is the main motivation to be able to model uncertainty in the model capacity or are there other reasons to strongly favour NPBayes? Answers:
** Eric Xing: NPBayes is also interesting because you are solving one problem while for model selection you have to solve many problems at once.
** David Blei: NPBayes also makes it easier to define prior distributions over combinatorial objects.
* Vikash Mansighka: asked about the role of consistency of infinite capacity models: aka. how much should we care about exchangeability and such. A long discussion followed from which I just recall that the statisticians in the panel all agreed that this is crucial and one should really spend time proving these properties.

Finally, the panel was asked how they see the future of NPBayes, some answers:
* Zoubin Ghahramani: believes we will see applications of NPBayes on very large problems,
* Yee Whye Teh: believes we will see more interesting use of optimization in NPBayes,
* Lawrence Carin: thinks we will have priors adapted to our custom applications, not just use the few building blocks (DP, IBP, ...) we have now,
* David Blei: believes we will see nonparametric distributions over more complicated combinatorial structures.
