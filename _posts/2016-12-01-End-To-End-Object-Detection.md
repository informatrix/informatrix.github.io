---
layout: post
title: Recent end-to-end object detection deep learning methods
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

### For SSP-net, why cannot it fine-tune the layers precede the spatial pyramid pooling? ###
Because the training is designed to train the model with the ROIs from different images, which is not efficient


## Fast-RCNN ##

The main contribution:

1. Training is `single-stage`, using a `multi-task` loss.
2. Training can update all network layers (comparing to SSP-net).

The questions:

1. For bounding-box regression, do we need output 4xK values for each class?
2. Spatial pyramid pooling structure, in fast-RCNN only one lever of pyramid, HxW bins, while in SSP-net there are hierarchical levers of pyramids.
3. For fine-tuning, how can hierarchical sampling become a contribution of the paper? And what's the detail of hierarchical sampling? and how SGD is implemeted regarding the sampling method?
4. For bounding-box regression, why is $$ t^k $$ defined to specify a scal-invariant translation and log-space height/width shift relative to an object proposal.