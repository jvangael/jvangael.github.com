---
layout: post
title: "The Elastic Compute Cloud (Amazon EC2)"
description: ""
category:
tags: [Large Scale ML]
---
{% include JB/setup %}

Today I ran into this interesting offering from Amazon called the elastic compute cloud. The idea is that you create an image that consists of your application, libraries and data and load it up to Amazon. They will run the application for you and charge you for the computing resources that you've consumed. I was a little suprised to see how cheap it actually is (in dollars): 0.10 for every hour that you run a process that consumes not more than 1.7 GB of memory, 160 GB storage; an extra 0.10 per gigabyte you transfer into their service and an extra 0.18 per gigabyte you transfer out of their service.

I think this is going to be a very useful platform for machine learning research. EC2 means that large scale map-reduce isn't just for Google anymore. Although I haven't tried it myself, creating the EC2 images should be straightforward as it is based on Xen virtualization; the virtualization platform out of our very own Cambridge computer lab.

I wonder why anyone would want to spend time and money on maintaining their own cluster when there is this cheap alternative available? As soon as I get the chance, I will run an experiment on Amazon EC2 and report on the experience.

PS [Data Wrangling](http://www.datawrangling.com/) has some good posts on how to use Amazon EC2.
