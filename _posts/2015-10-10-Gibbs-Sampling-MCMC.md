---
layout: post
title: Introduction to Gibbs Sampling and  Markov Chain Monte Carlo
---

In machine learning, you would see a lot of techniques borrowing from `statistical physics`, like the `mean field` used in variational inference. In this article, I will discuss one fundamental tool that is widely used in machine learning area, which is `Markov Chain Monte Carlo` (MCMC). MCMC is a popular simulation technique, which is popular in wall street. We should start from simple example.

### Monte Carlo Integration

It's easy to understand it with an example

$$
 I = \int g(\theta) p(\theta) d\theta
$$

The form is very common in statistics, for example it can be mean when $$g(\theta) = \theta$$  or variance $$g(\theta) = (\theta - E(\theta))^2$$. The point is that generally there is no close-form function. That would be a problem. Let us put a concret example, we would like to know the variance of the variable $$\theta$$. How did researcher already resolve the problem?

Actually, the idea is very simple -- just `do sampling`. We would estimate the average height of people by just looking at maybe randomly picked 1000 persons.

> I think approximation may be the most important concept in machine learning.

With the `sampling` idea, we can estimate  $$I$$ with $$M$$ random i.i.d samples.

$$
I = \frac{1}{M} \sum_{i=1}^M g(\theta^i)
$$

We often call it `Monte Carlo Integration`. You may wonder how accurate the sampling could be. It turns out to be quite satisfied. For example, let us look at the following function which is to compute the mean of Beta(3,5). It can be analytically solved

$$
E(\theta) = \int \theta p(\theta) d\theta =  \int \theta \frac{\tau(3+5)}{\tau(3)\tau(5)} \theta^2(1-\theta)^4 d\theta = \frac{3}{8}
$$

Now let's do sampling with `numpy` library in `Python`.

{% highlight python %}

>>> import numpy
>>> n=1000
>>> samples = numpy.random.beta(3,5,n)
>>> sum(samples)/n
0.37765878588500018

{% endhighlight%}

For lots of applications, the sampling results are quite acceptable.

> The independence is the key for the sampling method.


### Markov Chain
It seems quite simple to apply the sampling method, but life is not that easy. The challenge is how we can generate independent samples. `Markov Chain` is the tool that we need for the `independence`.


