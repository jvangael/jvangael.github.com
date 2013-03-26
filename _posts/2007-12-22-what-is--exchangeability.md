---
layout: post
title: "What is ... Exchangeability?"
description: ""
category:
tags: [Statistics]
---
{% include JB/setup %}

Talking about exchangeability, a friend once commented that exchangeability is "too simple too understand". On one hand, it is true that the statement of exchangeability (see below) sounds somewhat trivial, I found that I had absolutely no intuition as to why it is important for machine learning. So after some reading, I present my take on the concept of exchangeability.

### What is Exchangeability?

__Scenario 1.__ Imagine we have an urn with r red balls and b blue balls. We draw 3 balls from the urn as follows: we pick a random ball, write down its color and put it back in the urn before drawing a new ball. We introduce 3 random variables: A, B, C which denote the color of the first, second and third ball. It is not hard to see that $p(A=r, B=b, C=b) = p(A=b, B=r, C=b)$; in other words, we can exchange the values of the random variables without changing the joint probability. Intuitively, the reason we can exchange the observations is that our random variables are IID (independent and identically distributed).

__Scenario 2.__ We again pick 3 balls from an urn with r red and b blue balls. We still pick a random ball and note its color, but we put two balls of that color back in the urn. It may not be obvious that the sequence $A=r, B=b, C=b$ has the same probability as the sequence $A=b, B=b, C=r$ since the individual probabilities of picking the red ball first or last are completely different: $r/(r+b)$ when it is the first ball versus $r/(r+b+2)$ when it is the last ball (since two blue balls were added in the mean time). Writing down the equations makes it clear that the two sequence are equi-probable
$$ \frac{r}{r+b} \frac{b}{r+b+1} \frac{b + 1}{r+b+2} = \frac{b}{r+b} \frac{b+1}{r+b+1} \frac{r}{r+b+2}$$

It is trivial to generalize this expression to longer sequences. Again, it doesn't matter in what order we pick the balls, the only thing that matter is how many red and how many blue balls we pick. This is reflected in the formula in the sense that denominator of the probability of a sequence only depends on how long the sequence is. The nominator part only needs to know how many balls of each color there are. In our example: it only needs to know that there is a first and second blue ball (contributing $b * (b+1)$ to the nominator) and a first red ball (contributing $r$).

__Scenario 3.__ Both examples above were exchangeable since reordering the values of the random variables didn't change the probability. Let us consider a similar setup where exchangeability does not apply anymore. We again use the urn scheme with r red balls and b blue balls. However, now when we pick a red ball we note its color and simply put it back, but when we pick a blue ball we note its color and put two back. It is easy to see that we cannot exchange the value of the random variables anymore since

$$ p(A=r, B=b, C=b) = \frac{r}{r+b} \frac{b}{r+b} \frac{b+1}{r+b+1}$$
while
$$ p(A=b, B=b, C=r) = \frac{b}{r+b} \frac{b+1}{r+b+1} \frac{r}{r+b+1}$$

I think the following definition of exchangeability now becomes much more intuitive; we say a set of n random variables $Y$ is exchangeable under a distribution $p$ iff for any permutation $\pi$ of the integers $1..n: p(Y_1, \cdots, Y_n) = p(Y_{\pi_1}, \cdots, Y_{\pi_n})$

### Properties of Exchangeability

Let us now briefly discuss some consequences of exchangeability as it will allow us to see why it is such an important concept. First, we compute the marginal probability of the second draw $p(B = r)$ under the different scenarios. Under scenario 1 this is trivial, just before the second draw the content of our urn is exactly as it was when we started: hence $p(B=r) = r/(r+b)$. Under scenario 2, after some simple algebra we find that $p(B=r) = p(A=b, B=r) + p(A=r, B=r) = r/(r+b)$. Now here is the exciting part: we shouldn't have done all the algebra; if we are convinced that the random variables are exchangeable under the distribution of scenario 2, we could have acted as if we were computing the marginal probability for the first draw. Formally, since $p(A=b,B=r) = p(A=r, B=b)$ and substituting this in the expression for $p(B=r)$, we could have marginalized out the $B=b$ part. This property - changing the order around - is incredibly useful when computing probabilities.

More abstractly, here is one way to think of exchangeable sequences. In scenario 2, if a friend just drew a ball from the urn, didn't show it to us and put one extra ball back in the urn, this is not going to make a difference as to the probability of our next draw. However, in scenario 3 above, whether someone drew a ball before us is very important: it drastically changes the probabilities for our next draw. I think this is a very important distinction that sets exchangeable and non-exchangeable distributions appart.

Although exchangeability and IID variables look very similar they are not exactly the same. From scenario one above, it is easy to see that IID random variables are exchangeable. The converse is not true: in scenario 2, $p(A=b, B=r)$ is not equal to $p(A=b) p(B=r)$ and thus the random variables are not independently distributed.


### Exchangeability and Machine Learning

Exchangeable distributions are very common in machine learning. The most famous modelling assumption for text processing is just exchangeability: the bag of words model. This modelling assumption states that the probability of a text document depends only on word counts and not on word order. This is exactly the same model as scenario 1 above except that instead of red and blue balls, we now have words from a fixed vocabulary. Is this a realistic assumption one may ask? It certainly is not! We don't expect natural language to be exchangeable: the probability of using the word "States" should certainly be dependent on the word in front of it (a.k.a. higher if that word is "United"). But who cares, the bag of words assumption works incredibly well ...

There are many other exchangeable distributions in common use for machine learning: the Dirichlet Process and its Chinese Restaurant Process equivalent are exchangeable distributions, the Indian Buffet Process is an exchangeable distribution on binary matrices. Non-exchangeable distribution are also common: many Markov models (e.g. Hidden Markov Models) aren't exchangeable.


I hope this little overview of exchangeability was useful. I left one improtant concept out of our discussion so far: De Finetti's theorem. This is a very important theorem that applies to exchangeable sequences and I will discuss the theorem in a future post.
