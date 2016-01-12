---
layout: post
title: Introduction to Information theory
---


Compression
==========
`Informaiton` is all we care about when interacting with the world. Before processing the informaiton, the first thing we need to do is to store the information inside our computer. For example, after you take a picture, how should we store that picture to maintain the most informative message and minimum the storage cost? The most straightforward method to store a gray image is just to store every pixel of image with 8 bits. We can ask two questions regarding the naive approach?

1. Can we have a better way to store exactly the same image without any lossing, but with less space?
2. Suppose we tolerate the lossness, how can we compress the image to save the space?

Fourier Analysis
================
