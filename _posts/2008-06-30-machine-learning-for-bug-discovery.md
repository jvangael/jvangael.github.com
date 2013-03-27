---
layout: post
title: "Machine Learning for Bug Discovery"
description: ""
category:
tags: [Machine Learning]
---
{% include JB/setup %}

_One of the reasons I have this blog is to talk about some of my own research. I intend to give some more background on things that haven't made it into a paper, put some more experiments or references online, answer questions people have about my work, ... I hope that by putting these discussions online, I can catch the attention of Google's indexer and this information is available for anyone who might ever work on similar things._

Today we, [Finale Doshi](http://mlg.eng.cam.ac.uk/finale/) and I, want to talk about a small side project of ours. Early this year we ran into a pretty cool project at the University of Wisconsin - Madison called the [Cooperative Bug Isolation](http://www.cs.wisc.edu/cbi/) project. In a nutshell, this project aims to find software bugs by first instrumenting the source code with little probes. These probes count when certain events - such as the execution of a particular line of code - occur.  The CBI software collects these probe counts, and remembers whether the program exited successfully or whether the program crashed. For example: imagine we wrote the following program:

    function foo()
    a = read_line()
    if a &lt; 10 then
      print "smaller than 10"
      a = 10 / a - a
    else
      print "at least 10"
    return a

Although this program is completely trivial, it has a potential division by zero. The CBI software will take a piece of source code as above and add some probes:

    function foo()
    a = read_line()
    log( a == 0, probe_1)
    if a &lt; 10 then
      print "smaller than 10"
      a = 10 / a - a
      log( a == 0, probe_2)
    else
      print "at least 10"
    log( a == 0, probe_3)
    return a

Note that there is a whole science to what probes are useful and where to put them, but the main point is that each probe is a counter, which gets augmented every time its first argument is true. As we mentioned above, when a program executes,various probes get augmented and at the end of the execution, the counts are stored in a file in addition to a flag that says whether the program exited gracefully or whether it crashed.

Let's suppose that foo is called several times in a larger program. After running that program a couple of times, we might get data that looks like this:

| Run | Probe 1 | Probe 2  | Probe 3 | Exit Flag
| ------ | ------ | ----- | ----- | ----- |
|  1  |  0  |   1  | 2 | Good |
|  2  |  1  |   2  | 2 | Fail |
|  3  |  0  |   5  | 1 | Good |

The CBI project has collected thousands of traces for different open source projects. The goal now is to mine these huge datasets to discover bugs in the source code. Although there are many ways of going about it, one way is to make the following assumption: if we run a program, we are executing a sequence of complex but fairly atomic "usage patterns". For example, imagine we are executing a web browser: when we press the homepage button a series of functions gets executed (and the corresponding counters are augmented). However, when we press the back button a different (but maybe overlapping) sequence of functions will be executed. We call these sequences "usage patterns".

In [this paper](http://pages.cs.wisc.edu/~jerryzhu/pub/rlda.pdf), some Programming Language and Machine Learning people in Madison (David Andrzejewski, Anne Mulhern, Ben Liblit, and [Jerry Zhu](http://pages.cs.wisc.edu/~jerryzhu/)) developed a statistical model (called DeltaLDA) based on Latent Dirichlet Allocation to learn two sets of usage patterns at the same time: one set of "good" usage patterns which both successful and failed runs use, and an extra set of "bad" usage patterns which only occur in failed runs. After learning the DeltaLDA model, one can go back and look at the bad usage patterns and see which counters are expressed. Since the counters in bad usage patters correlate with programs crashing, these could then be indicative of actual bugs in the source code. It turns out that it is a reasonable idea; read the DeltaLDA paper for details on how it performs in practice.

When we decided to work with this dataset, one obvious extension of the DeltaLDA model was to try and make the whole thing non-parametric. In the original DeltaLDA paper, one has to specify the number of usage patterns beforehand. We think this is unrealistic and allowing the number of usage patterns to adapt according to the data seems to be the right way to go. So we developed a model called the DeltaHDP which is exactly this: a non-parametric extension of DeltaLDA using the Hierarchical Dirichlet Process framework. On some of the smaller datasets which we tried, we found that the DeltaHDP behaved exactly as one would expect: it finds similar usage patterns as DeltaLDA but you don't have to specify the number of usage patterns beforehand. One other nice thing about the DeltaHDP is that the Gibbs sampler, which is fairly straightforward to implement, performs well.

Another unrealistic artifact of both the LDA/HDP type models is that the corresponding generative model does not correspond to the usage pattern story above. LDA/HDP define each run of a program to be a mixture of usage patterns while we really want each run to be an integer combination of usage patterns. The reason is that we believe that each time a usage pattern is executed, it augments the counter more or less deterministically - counters do not randomly fail to increment. In the end, we came up with a model based on the Indian Buffet Process. Check out [our poster](http://mlg.eng.cam.ac.uk/jurgen/pubs/crism2008bug.pdf) for more information on the model. It turned out the inference was a little nightmare and we never found a good sampling mechanism which could scale to very large datasets. However, the results on smaller datasets suggested that the model was OK and we got similar results as the DeltaHDP. In addition, the IBP returns more information: it can tell you exactly how many times specific usage patterns were executed whereas the DeltaHDP only returns the ratio that each usage pattern was executed.

In the end it was a fun project. We enjoyed working on this data, had a lot of fun coming up with the models and we learned a lot about non-parametric methods. Unfortunately, both Finale and I have different priorities and we think the cooperative bug isolation project deserves 100% of one's attention to make progress on using statistical models for bug isolation. However, we think CBI is a great project, and we will be more than happy to give some more background on our models and answer questions about our experiences.
