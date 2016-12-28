---
layout: post
title: Recent end-to-end object detection deep learning method
---

Deep learning has really boosted the application of compute vision.

There are a few guys who are quite active in the research community.

Some fundamental questions:

1.What does the response in the feature map really mean? Means some feature being activated?

2.Is CNN recognizing the object by their shape information?


## RCNN ##



## SSP-net ##
Spatial Pyramid Pooling in Deep Convolutional Networks for visual Recognition (SSP-net)

For SSP-net, what does each spatial bin really contribute to the final results?

For SSP-net, why cannot it fine-tune the layers precede the spatial pyramid pooling?


##Fast-RCNN##

The main contribution:

1. Training is `single-stage`, using a `multi-task` loss.
2. Training can update all network layers (comparing to SSP-net).

The questions:

1. For bounding-box regression, do we need output 4xK values for each class?
2.
