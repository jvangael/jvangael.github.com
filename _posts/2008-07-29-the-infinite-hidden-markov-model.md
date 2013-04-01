---
layout: post
title: "The Infinite Hidden Markov Model"
description: ""
category:
tags: [iHMM]
---
{% include JB/setup %}

I am at ICML two weeks ago I presented some of our work on the infinite hidden Markov model (also known as iHMM or HDP-HMM). Together with a result from Emily Fox, I believe we have come full circle and it is time for a little summary.

[Hidden Markov models](http://en.wikipedia.org/wiki/Hidden_Markov_model) have been the workhorse of the discrete time, discrete state time series community for over 40 years. We have seen applications in speech, robotics, natural language processing, vision, ... Sometimes, domain knowledge can be used to choose the dimensionality of the latent state space, but very frequently there is no reason to prefer one dimension over the other. Moreover, maybe we explicitly want to model the uncertainty in the dimensionality of the latent state space! Hence, variational Bayes, BIC or other model selection techniques do not apply and one option is to turn to infinite capacity models.

In 2002, Matt Beal, Zoubin Ghahramani and Carl Rasmussen [introduced](http://books.nips.cc/papers/files/nips14/AA01.pdf) a first version of an infinite capacity model which they called the iHMM. Their proposal is a procedure based on a two level hierarchy of urns which generates a potentially infinite transition matrix. Although it is an extremely elegant proposal, it turned out to be pretty hard to come up with a correct and efficient sampling scheme to learn this model. The model has three parameters: one to control the number of states, one to control the sparsity of the transition matrix and one to control the self transition probability.

Then, in 2006, Yee Whye Teh, Mike Jordan, Matt Beal and Dave Blei introduced the [Hierarchical Dirichlet Process](http://www.gatsby.ucl.ac.uk/~ywteh/research/npbayes/hdp2004.pdf). The HDP is a very natural prior for building hierarchies of clusters: in other words, cluster datapoints in different groups so that clusters are shared between groups. Although the HDP is technically a bit complex, it is theoretically well founded and in the 2006 paper a relatively efficient Gibbs sampling scheme was introduced. In the same 2006 paper, an infinite capacity hidden Markov model was built on top of the HDP. This model is very close to the original iHMM but only had two parameters: the self transition control was left out. This is unfortunate as for many applications of HMM's (changepoint detection) we know a priori that the Markov model is going to stay in the same state. Finally, this "version 2.0" of the iHMM still only used a Gibbs sampling scheme for inference. This is unfortunate as we have [come to understand](http://www.jstor.org/pss/3085787) that Gibbs sampling can perform poorly in time series models.

Enter ICML 2008: the first iHMM related result was a paper by Emily Fox, Erik Sudderth, Michael Jordan, and Alan Willsky called "An HDP-HMM for Systems with State Persistence". In this paper, the "version 2.0" iHMM model was extended to include the self transition parameter again. As you can read in their paper, this makes a very big difference: combined with some other neat ideas they were able to present some impressive performance on speaker diarization. Next, was our (Jurgen Van Gael, Yunus Saatci, Yee Whye Teh, and Zoubin Ghahramani) paper called [Beam Sampling for the Infinite Hidden Markov Model](http://mlg.eng.cam.ac.uk/jurgen/pubs/icml2008ihmm.pdf). The main idea in our work is to use a slice sampling scheme to adaptively truncate the infinite model to a finite model. This then allows us to run a dynamic program and resample the whole state sequence at once. Although we've only presented the beam sampler in the context of the iHMM, the technique is applicable to most nonparametric constructions I know of. One thing that I hope will happen is that someone will try to use the slice sampling technique to cut up nonparametric models into finite models, and use our best inference machinery (variational, BP, EP, ...) to perform inference in the finite model. This would allow us to leverage all the knowledge we've built up for finite graphical models and use them in the nonparametric setting.

Stepping back and taking a bird's eye view on things: I think that after the four iHMM papers, I think we now have a strong platform to start using the iHMM as a building block in more complicated models. At the NPBayes workshop we've already seen some [cool results](http://www.gatsby.ucl.ac.uk/~ywteh/npbayes2008/abstracts/Fox.pdf) by Emily who uses the iHMM to switch between different auto-regressive processes and linear dynamic systems. Another trivial extension which we've implemented is to create an IO-iHMM: condition the iHMM on a certain input sequence. [Finale](http://mlg.eng.cam.ac.uk/finale/) and I are currently experimenting with this setup for learning infinite POMDP's; more about that in a future post. I've been promised that more interesting extensions are in the making ... let's see what NIPS brings!

As I have to write up a first year report (Cambridge's idea of a thesis proposal), I have been thinking very hard about a short, self contained and easy explanation of the iHMM. A description of the model so everyone can use and implement it without having to work through the whole HDP formalism. I will definitely post the outcome on my webpage early September. At least one cool spin-off has come out of this report: based on a suggestion by [Radford Neil](http://www.cs.toronto.edu/~radford/), we've come up with a different dynamic programming based sampling scheme based on the [embedded HMM](http://www.cs.toronto.edu/~radford/ftp/emb-hmm-nips.pdf). As it is more incremental work, I will probably only describe it in my first year report and this blog so stay tuned ...