---
layout: post
title: "Beginner in Deep Learning"
date: 2016-01-09
---

Deep learning has been popular in both industry and academic for quite a while. It is so impressive that every machine learning position would ask you about the `deep learning`. It is not exaggerated to say that machine learning has been dominated by deep learning now. The success of deep learning can be attributed to the modern inference algorithms.

With the background of `Gaussian process`, I am always curious to figure out the connection between GP and DP, while currently there is not much work that tries to improve each other from leveraging modern research achievements of each side. I will write down what I have learned and thought about while diving into deep learning. Hope it can also help someone who is a novice like me.


Fundamental Concepts
-------------------

Function  $$ f(x)$$
====================

With the background of computer science, I have almost forgotten what the function is about after 4 years of intensive training. In CS, function is a slice of code which can be reused in the program. We need to change our view about funciton in `machine learning` area. Funciton is more about the description of the physical world. For example, we can say your decision about where to go for lunch is based on some variables, like budget, preference, schedule and so on. Right now, it is the only programmable way we can model our world. And the machine learning is all about `functioin regression`, which is to find a function that can generate our physical world. The procedure about infering the function is mainly done by `optimization`. The idea is that the data observed provides some portion of the function, we need to make our guess function as close as possible to visible function.

Why features matter
==================

It takes me a long time to understand the importance of the features. With minor background of mathematics, you may know the `linear` and `non-linear` function. We are good at training the linear function, which is a `line fit` in 2D. `Non-linear` can be thought as a `curve-fit` in 2D, which is much harder. For example, let us look at two functions

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

So the feature construction goal is to find the feature that can contain more information which contributes to the function and reduce the nonlinearity of the target function. Normally, the input features to the machine learning algorithm is not very informative, we let the model to decide how to use those feeding features.

How to do optimizaiton
======================

Don't worry, if you have no background on optimizaiton research. It is much similiar as you climb the hill. How do you do `hill climbing`? Is there any algorithm which can guarantee that you can get the peak of hill? The most heuristic way is just to guarantee that you never go down the hill. For most real applications, there are no mutual methods which can guarantee that we can always get the `global maximum point`. The optmization techniques are about how we take each step to get closer to our target, which means reduce the `cost function`. As long as each step we are reducing the cost function, or in other words we are getting better, we can finally achieve our goal. Optmization research is about how to speed up the climbing procedure and how to get `global optimal point`. For example, modern `stochastic gradient descent` method is a randomized approach to do optimization. The hindsight is that the method can also guarantee that each step we are reducing the cost funciton, and every step is super fast than other methods althought it may just be a little improvement. It is a trade-off between a griant but costy step and a minor but fast step. You can find more details about optmization in another post [Introduce to optimization]({% post_url 2015-11-07-Introduce-to-Optimization %})

Linear algebra is important for modern machine learning
======================================================

The linear algebra course was taken during my first semester in undergraduate study. And it is really aweful because of the way the professor conducted the courses. To work with `high-dimensional` data, linear algebra is the most important and useful tool. To do well in machine learning, it's necessary to master linear algebra. The top material is the Gilbert Strang's open course [linear algebra](http://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/) from MIT, which is indeed intuitive and applicable.

I have studied lots of linear algebra by myself. The first inspiration is its applicaiton in multimedia or `computer vision`. The `foundation in multimedia` conducted by [Prof. Terence Sim](https://www.comp.nus.edu.sg/~tsim/) is the best course I have ever taken during my graduate study in NUS. Here is my note about [linear algebra]({% post_url 2015-11-01-Introduce-to-Linear-Algebra %})

Probability is getting more intensions
=====================================
The last important tool that has been intensively used in machine learning is probability. Somehow we can treat the learning as a statistical learning process. Actually what we are doing is just to pick the most likely results based on our observation (`evidence`) and our prior. You can apply `Bayes rule` everywhere, it is the principle way to incorporate our human bias.

Approximation
=================================
Long before I studied machine learning, I thought everything about science is 100% true or accurate. It turns out to be wrong. Science is really about `approximation`, where we propose some guess and these guess can be generalized well to explain our daily observation. The idea is very important to understand lots of modern learning algorithms, especially in the area of computational optimization.

Big data 
==========================
Now everyone talks about big data. The following picture can give you a rough reason why it makes sense. With more informative data, we can just run simple algorithm to get much better results.

![bigdata](/image/learning.jpg)


Anyway, machine learning is just a tool that is developed to solve the problem. `What's more useful than tool itself is the way of thinking about our physical world`. To summary, we can model the world information using math. The approach is to find a proper function in the massive function space, and parameter is the way to control the freedom of the function space. This is our world, it's all about `information`. 


