---
layout: post
title: "Beginner in Deep Learning"
date: 2016-01-09
---

Deep learning has been popular in both industry and academic for quite a while. It is so impressive that every machine learning position would ask you about the `deep learning`. It is not exaggerated to say that machine learning has been dominated by deep learning now. The success of deep learning can be attributed to the modern inference algorithms.

With the background of `Gaussian process`, I am always to figure out the connection between GP and DP, while currently there is not much work that tries to improve each other from leveraging modern research achievement of each side. I will write down what I have learned and thought about while diving into deep learning. Hope it can also help someone who is the beginner like me.


Fundamental Concepts
-------------------

Function  $$ f(x)$$
====================

With the background of computer science, I have almost forgotten what the function is about after 4 years of intensive training. In CS, function is a slice of code which can be reused in the program. We need to change our view about funciton in `machine learning` area. Funciton is more about the description of the physical world. For example, we can say your decision about where to go for lunch is based on some variables, like budget, preference, schedule and so on. Right now, it is only the only programmable way we can model our world. And the machine learning is all about `functioin regression`, which is to find a function that can generate our physical world. The procedure about infering the function is mainly done by `optimization`. The idea is that the data observed provides some portion of the function, we need to make our guess function as close as possible to visible function.

Why features matter
==================

It takes me a long time to understand the importance of the features. With minor background of mathematics, you may know the `linear` and `non-linear` function. We are good at training the linear function, which is a `line fit` in 2D. `Non-linear` can be thought as a `curve-fit` in 2D. For example, let us look at two functions

* Liner function $$y$$

$$
y = ax  + b \tag{1}\label{1}
$$

* Nonlinear function $$y$$

$$
y = a_1 x +  a_2 x^2 + b \tag{2}\label{2}
$$

It seems that nonlinear function (\ref{2}) is more complicated than linear function (\ref{1}). And that is also almost true for problem modeling. However, image that if we have a `super feature` $$f(x) = (a_1 x + a_2 x^2)/c$$ in hand, then the nonlinear problem can be converted into linear problem

$$
y = c f(x) + b \tag{3}
$$

So the feature construction goal is to find the feature that can contain more information which can reduce the nonlinearity of the target function.
