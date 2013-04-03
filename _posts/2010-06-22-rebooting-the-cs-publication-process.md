---
layout: post
title: "Rebooting the CS Publication Process"
description: ""
category:
tags: [Rants]
---
{% include JB/setup %}

Dan Wallach makes suggestions for revolutionizing the CS publication process in [this 13 page report](http://www.cs.rice.edu/~dwallach/pub/reboot-2010-06-14.pdf). I really like this stuff and can only hope things start moving sooner rather than later in this area.

On the time of reviewing, a recent paper I really enjoyed is[ Novel Tools To Streamline the Conference Review Process: Experiences from SIGKDD'09](http://research.microsoft.com/pubs/122784/ReviewerCalibration.pdf) by a Bristol/MSR collaboration. For me the most interesting part of the paper was a probabilistic graphical model which collaboratively learns how to calibrate reviewers. Calibration here means that we’d like to understand how different reviewers have different thresholds for giving a paper 1/2/3/4/5 star reviews. The generative model proposed in the paper can easily be implemented in Infer.NET and although it is perhaps to early to make decisions based on the method, it could certainly help PC’s in making their decisions.
