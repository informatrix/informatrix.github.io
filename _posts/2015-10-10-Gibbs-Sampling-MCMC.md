---
layout: post
title: Introduction to Gibbs Sampling and  Markov Chain Monte Carlo
---

In machine learning, you would see a lot of techniques borrowing from `statistical physics`, like the `mean field` used in variational inference. In this article, I will discuss one fundamental tool that is widely used in machine learning area, which is `Markov Chain Monte Carlo` (MCMC). MCMC is a popular simulation technique, and really successful in wall street. We should start from the simple example.

### Monte Carlo Integration

It's easy to understand it with an example

$$
 I = \int g(\theta) p(\theta) d\theta
$$

The form is very common in statistics, for example it can be mean when $$g(\theta) = \theta$$  or variance $$g(\theta) = (\theta - E(\theta))^2$$. The point is that generally there is no close-form function. That would be a problem. Let us put a concret example, we would like to know the variance of the variable $$\theta$$. How did researcher resolve the problem?

Actually, the idea is very simple -- just `do sampling`, like what we estimate the average height of people by just looking at maybe randomly picked 1000 persons.

> I think approximation may be the most important concept in machine learning.

With the `sampling` idea, we can estimate  $$I$$ with $$M$$ random i.i.d samples.

$$
I = \frac{1}{M} \sum_{i=1}^M g(\theta^i)
$$

We often call it `Monte Carlo Integration`. You may wonder how accurate the sampling method could be. It turns out to be quite satisfied. For example, let us look at the following function which is to compute the mean of Beta(3,5). It can be analytically solved

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
It seems quite simple to apply the sampling method, but life is not that easy. The challenge is how we can generate independent samples. `Markov Chain` is the tool that can help to mitigate the generation process. It's not that straightforward to understand why Markov Chain works here.

First, let's define the `Markov Chain` itself:


>Markov Chain is a random process in which future states are independent of past states given the present state.

The transition between the states is governed by a **transition kernel**, which like

![transitionkernel](/image/transitionkernel.png){: .center-image}

. $$p(\theta^{t+1}_{A} \shortmid \theta^{t}_{B})$$ means the probability of next state would be  $$\theta_{A}$$ given current state is $$\theta_B$$.

Here is how Markov Chain work.

1. Start from a distribution and get samples $$\theta^0_i \sim \pi^0, i = 1,\ldots, M$$.
2. Recusively compute the next samples set based on the transition kernel, $$\pi^{t+1} = \pi^{t} P $$

In Bayesian statistics, we usually assume that there is a stationary distribution for $$\pi$$, which means

$$
\pi = \pi P
$$

Now, it's clear that we want to approximate our desired distribution $$p(\theta)$$ with $$\pi$$. Once Markov chain converges to the stationary distribution, and the samples in our chain would like to be draws from $$p(\theta)$$. It's enough for you to understand what MCMC is doing. For more curious readers, it's time to dive into more details about how to choose the samples and make the algorithm more rubust.

#### Ergodic Theorem
There are three requirements for MCMC methods to approach the exact value with probability 1.

1. Aperiodic
2. Irreducible
3. Positive recurrent

With above properties, the `MCMC` samples which are slightly dependent can still be used to simulate the distribution $$p(\theta)$$. Next we would take about one MCMC algorithms--- Gibbs sampling.

### Gibbs
Josiah Willard Gibbs is an American scientist, who received the first US PH.D in engineering. Together with Maxwell and Boltzmann, he created `statistical mechanics` where the Gibbs sampling came from.



