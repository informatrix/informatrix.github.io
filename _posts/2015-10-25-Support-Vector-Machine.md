---
layout: post
title: Support Vector Machine
---

I have struggled a lot to understand what `support vector machine` is. But because SVM is never my own topic, I am never able to find some time to figure it out. Now since I don't have any research task, I finally get time to figure out what is inside `SVM`.

The essential part about SVM is that the model is trying to find some support vectors that can decide the boundary. In this article, I mainly summarize the SVM notes from Andrew Ng's [Machine Learning](http://cs229.stanford.edu/notes/cs229-notes3.pdf)

## Intuition: Margins #

It is important to think about 2D first. After understadning SVM in 2D completely, it is easy to be generalizd well to high-dimensionality. Let's look at the concret problem of classification.

![SVM](/image/svm1.png){: height="300px" .center-image}

We should start with the simple `linear-separable` one, where there exists a line which can separate the two different classes. The line can be expressed as $$wx + b = 0$$. The points those falls above the line would be classified as 1, and the points below the line would be classified as -1. The idea can be formalized as

$$
h(x) = g(wx + b)
$$

where $$g(z) = 1$$ if $$z \ge 0$$ and $$g(z) = -1$$ otherwise. Next, we need to model our target function. There are two ways to look at it.

### Functional Margin

The first intuitive way to express the target is by using the prediciton confidence. We would be more confident about our prediction when the point is far above the line, which means that we hope that the `functional margin` $$t(x) = y g(wx + b)$$ could be as large as possible. $$y \in \{1, -1\}$$ is the lable of the points. When $$y = -1$$, we know that $$g(wx+b) < 0$$ , so we still have $$t(x) > 0$$. In both cases, we can formalize the problem as 


### Geometric Margin

The next intuitive perspective is based on geometric margin. The basic idea is that we try to maximize the `geometric margin`.

![SVM2](/image/svm2.png){: height="300px" .center-image}



