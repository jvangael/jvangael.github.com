---
layout: post
title: "To R or not to R"
description: ""
category:
tags: [Machine Learning,Statistics,R]
---
{% include JB/setup %}

At the moment 90% of the research in our lab is done using Matlab. Some of us have tried Python but were dissapointed by how hard it was to get decent (read: native) numerical routines on par with Matlab. I've been developing on the .NET platform with a little bit of Java development (for Amazon's Elastic Map-Reduce) on the side. We've had a few discussions in our lab recently about switching to R for our machine learning research. A decision hasn't been made and we're wondering what the larger machine learning community thinks about this issue. Here's a list of pros and cons that I've come up with

Pros:
* great support for statistical functions
* great support from the statistical community
* good (if not better) plotting that Matlab
* reasonable fast (check out [Dave's](http://mlg.eng.cam.ac.uk/dave/) [benchmarking](http://mlg.eng.cam.ac.uk/dave/rmbenchmark.php))
* free (very important!) if we want to run a job on 100 machines (e.g. in the cloud), I believe currently you need a matlab licence for each one

Cons:
* pre-historic interface, doesn't compare to modern IDE's
* debugging doesn't seem up to Matlab standards
* not much support in machine learning community (?)
* learning curve

The jury is still out on this one ... I really wonder how many machine learners out there already use R?