---
layout: post
title: "London Machine Learning Meetup ... and joining a startup."
description: ""
category:
tags: [Machine Learning,Meetup,Microsoft,Rangespan]
---
{% include JB/setup %}

Three months ago I decided to end my employment at Microsoft. I had a great time, met loads of interesting people and will definitely miss being in the Cambridge research lab (as well as the occasional trip to Seattle).

Next up I am joining a startup company called [Rangespan](http://www.rangespan.com/). I met the founders of Rangespan at [Silicon Milkroundabout](http://siliconmilkroundabout.com/) in April this year. When I got talking to them it was immediately obvious there was a hell of a lot of machine learning to be done there.

Rangespan is essentially an e-commerce platform which is organizing a marketplace for suppliers to sell products to big retailers. On one hand Rangespan is trying to build the biggest catalog in the world. We're doing some by fusing many different information sources (supplier feeds, manufacturer feeds, crowdsourced data, crawled data). The three big learning problems in this space are:

* __Matching__: out of millions of product descriptions (semi-structured &amp; textual), how do you recognize which descriptions talk about the same product? _Record linkage is the keyword here, but making it work at large scale and under very small precision and recall margins is a challenge._
* __Reconcilliation__: when you have 100 different descriptions of a product, and you want to construct the best possible description of the product, how do you do that? _I think the speech recognition and machine translation community has a few neat tricks up their sleeve to be applied here: in the abstract if we think of each of the 100 descriptions as the output of a noisy channel with the unknown ground truth description as the input, the challenge is to invent a prior and model for the noisy channel. Machine learning baby!_
* __Information Extraction__: the data we are gathering is only semi-structured and most often marketing text. The question now becomes: how do we figure out form a USB stick description that the product has a "4GB" capacity. How do we figure out that "4GB" is the same as "four gigabytes" etc etc. _There's loads of great work on information extraction which we can build on; the good news is that our domain is restricted (physical goods) the bad news is that the domain is quite large (1000's of categories, 1000's of attributes)._

Besides the catalog, Rangespan is also building an order pipeline component. One crucial component of that pipeline is the system that assigns retailer's orders to suppliers. The idea here is that for each product we have a pretty good view of the supply curve (what suppliers sells how many items at what price). We also have a pretty good view of the demand curve: by aggregating many different retailers we can predict what the demand for a product will be. This allows us to make very quantitative decisions about how to choose the price for that product to optimize metrics like user experience etc. In this area a mix of statistics (time series analysis), decision theory, econometrics and optimization are crucial ingredients ... together with a ton of data ofcourse.

If this all sounds like music to your ears, then let us know. We're [hiring](http://www.rangespan.com/jobs/)!

Joining a startup also meant I am now working in London. One of the coolest things I discovered about being in London is the great number of meetups people are organizing. From MongoDB office hours (thank you for all the help 10gen!) to the [Hadoop](http://www.meetup.com/hadoop-users-group-uk/) and [Big Data](http://www.meetup.com/big-data-london/) meetups. Although big data is crucial at Rangespan, we think clever algorithms (as in machine learning) are as crucial to building successful insights from data. As such we are kicking off the [Machine Learning Meetup](http://www.meetup.com/London-Machine-Learning-Interest-Group/) as of January 2012. We'll put some fun talks together with the London machine learning community and probably do some study groups on the Stanford online learning courses.

If you live closeby and haven't yet signed up, you can find all meetup details here.
