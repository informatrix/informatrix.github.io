---
layout: post
title: Introduction to Information theory
---

# Compression #

`Informaiton` is all we care about when interacting with the world. How do we define `information`? What is it and how can we represent the information
? Before processing the informaiton, the first thing we need to do is to store the information inside our computer. For example, after you take a picture, how should we store that picture to maintain the most informative message and minimum the storage cost? The most straightforward method to store a gray image is just to store every pixel of image with 8 bits. We can ask two questions regarding the naive approach:

1. Can we have a better way to store exactly the same image without any lossing, but with less space?
2. Suppose we tolerate the lossness, how can we compress the image to save the space but to retain the most information?

## Information ##

For example, suppose we have an array of integers `a = [1,1,1,1,1]` or even an image with only pixels with value of 1, how should we store the information in the computer? Is there any formal way to say the minimum bits we have to store the information? Instead of listing every element of the array, we can represent the same array with two variables `[size, value]`.


Huffman Code
===========
We define the `information size` in terms of current computer implementated architecture, which is the number of bits used to store the information.
Suppose we want to store number `1` in the computer, we can encode it with one boolean, one integer or one Byte. Another example is that suppose we want to store a set of points $$ [x_1,2x_1], [x_2, 2x_2], [x_3, 2x_3], \ldots, [x_n, 2x_n] $$, the naive way is just to store them as a two-dimensional array of `int`. Is there any better way? Yes, we can have a more compact representation, which is $$ [x_1,x_2,x_3,\ldots,x_n] $$ plus a linear function with weight `2`. Machine learning is the way to store the information in a compact way by using the mathematical model. For example, in the nearest neighbour classifier, we don't have any training part, for each prediction we just scan the training dataset, to find the most likely or nearest one, which is slow when scaling up. The analogy is the `index` idea in data structure. Without `index`, we need to scan the whole array to search one item. With `index`, we can retrive the item immediately. The model training is the proceduce to build the `informaiton index` system. And the prediction is like to compute the hash code.

The idea can be extended to more complicated index, which is to model the function using a serie of basic function, in another terms, an infinite dimensional vector space. One of most popular example is Fourier transformation. Another application of function analysis is to do compressioin. As we know, we can get the minimum encoding bits if the distribution has a low entropy. With this idea, we can approximate the raw signal/image to obtain an approximated result + some error (where error is with low entropy). Then we can have a good compression result. 



Fourier Analysis
================
