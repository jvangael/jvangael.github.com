---
layout: post
title: "F# and the Task Parallel Library"
description: ""
category:
tags: [F#]
---
{% include JB/setup %}

In a previous post I discussed how F\# asynchronous workflows can be used for parallelizing computations. More specifically, I chose to work with the standard matrix multiplication algorithm as it illustrates the point of how easy it is with F\# to take some existing (embarrassingly parallelizable) code and actually parallelizing it. Although F\# asynchronous workflows can be used for parallelization, they are really designed for helping with asynchronous I/O for reactive programs.

Enter the Microsoft Parallel Extenions for .NET 3.5. This is a very exciting new technology that is specifically tailored to please developers who are keen to learn how to use the quad-core machines they are sitting at. In other words, the parallel extensions are a new concurrency library which, to my best knowledge, is well suited for parallizing scientific applications. Although I haven't played around with features like PLinq, I did look a bit into the task parallel library (TPL) component of the parallel extensions. The TPL library makes our life easier by providing sophisticated algorithms for dynamic work distribution. In the following example I used the Parallel.For class to parallelize the matrix multiplication algorithm from my previous blog post.

{% highlight fsharp %}

let PFXMultiply (A: float[,]) (B: float[,]) =
  let n = Array2.length1 A
  let C = Array2.create n n 0.0
  let RowTask i =
    for j=0 to n-1 do
      for k=0 to n-1 do
        C.[i,j] <- C.[i,j] + A.[i,k] * B.[k,j]
    ()
  Parallel.For(0, (n-1), new Action(RowTask))
  C

{% endhighlight %}

As you can see, there is not much to to it. You just create the method which you want to execute in parallel (RowTask in our case) and pass it to the Action class which creates a delegate for you and passes it along to the TPL.

Here are the results when running the parallel matrix multiply for a 1000 by 1000 matrix on my quad core 2.4GHz machine: non-parallel version: 19.2 seconds, async version: 5.6 seconds, TPL version: 5.2 seconds. Feel free to download this file to play with it yourself.

Stay tuned for more neat (machine learning) applications of the TPL.
