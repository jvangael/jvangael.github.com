---
layout: post
title: "The Unreasonable Effectiveness of Data"
description: ""
category:
tags: [Large Scale ML]
---
{% include JB/setup %}

Alon Halevy, Peter Norvig, and Fernando Pereira (from the Google) just wrote an intriguing article called [The Unreasonable Effectiveness of Data](http://www.computer.org/portal/cms_docs_intelligent/intelligent/homepage/2009/x2exp.pdf) in IEEE Intelligent Systems. They argue a few points: 1) use more data to increase the performance of our learning algorithms, don’t make your models to complex; 2) the semantic web is not the right approach, it’s too expensive to “label” the web with its semantics, we need to learn it. However for an non-parametric Bayes person this is what got me very excited:

So, follow the data. Choose a representation that can use unsupervised learning on unlabeled data, which is so much more plentiful than labeled data. Represent all the data with a nonparametric model rather than trying to summarize it with a parametric model, because with very large data sources, the data holds a lot of detail.
