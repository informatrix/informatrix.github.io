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

TODO: understand the loss function defintion, and why use smooth L1 function?

Two ways of achieving scale invariant object detection:

* `brute-force` learning: each image is processed as a pre-defined pixel size during both training and testing. The network must directly learn scale-invariant object detection from the traning data. And it's proved by experiments that this approach is better. 
* `image pyramids`: providing approximate scale-invariance to the network through an image pyramid. Figure out implementation detail.

Why we need the distributed training?
If one model need to train more than one hours, then it's prohibitable to try many different methods or functions which may improve the model.

Another Trick: Truncated SVD for faster detection (Approximation idea).

Exact model & approximated solution vs. Approximated model &exact solution

Idea: figure out which layer is task dependent, then it need to be fine-tuned when learning the specific task. Otherwise, it can be shared among different task. Usually, the first layer is task independent (a well known fact).

## Faster RCNN ##

The main bottleneck for the detection using fast RCNN is the region proposal. And usually the region proposal is done in CPU instead of GPU. The idea is to speed up the region proposal by making advantage of GPU.


Idea: `sharing computation of convolutions which is efficient, yet accurate method for visual recognition.

Region Proposal Network is still doing the sliding windows, but based on the convolutional layer, which shares the computation with the detection. Also notice that the anchor plays the role of pyramid.

One challenge of detection is to handle the translation-invariant issue. It's easy to understand that the convolutional layer can be shift-invariant, but how to understand that the layer can be scale-invariant.

THe design of multi-scale anchors is a key component for sharing features without extra cost for addressing scales.

Also be careful about the selection of positive and negative samples.

a set of $$ k $$ bounding-box regressors are learned ?

Training RPN & Fast RCNN. The basic idea is to use deep nets to extract the features which can be shared between the proposal network and detection network.

Bounding-box regression is important for classification.

Implementation detail: number of proposals , scales, ratios (anchor) , choose the negative samples.

One idea about the end-to-end learning framework is that if we have a model with large capability, then more accuracy can be obtained when feed more data into the model.


## YOLO ##

Frame object detection as a regression problem to spatially separated bounding boxes and associated class probabilities.

The main idea for detection is how to perform bounding box and class probabilities prediction based on the feature sharing,

Encode contextual information about classes. (How to encode the global information of the image). Fast RCNN cannot.

Grid cell, and do regression on each cell to predict the probability of the class. And like DPM, it can model the size and shape of the objects. 

Compare `faster RCNN` and `YOLO`.

YOLO is good at proposal.

YOLO struggles with small objects compared to its closest competitors.

Implementation: Pr(Class| Object) only predict one set of class probabilities per grid cell, regardless of the number of boxes B, why?

To summary: the idea of the yolo is to sharing the 7 x 7 image classification problem, and cast the classification problem to be a regression problem. And 

## SSD ##

The first deep network based object detector which does not resample pixels or features for bounding box hypotheses and is as accurate as approaches that do.

Using a small convolutional filter to predict object categories and offsets in bounding box locations, using separate predictors (filters) for different aspect ratio detections, and applying these filters to multiple feature maps from the later stages of a network in order to perform detection at multiple scales.

1. The core of SSD is predicting category scores and box offsets for a fixed set of default bounding boxes using small convolutional filters applied to feature maps.
2. To achieve high detection accuracy we produce predictions of different scales from feature maps of different scales, and explicitly separate predictions by aspect ratio.


The SSD approach is based on a feed-forward convolutional network that produces a fixed-size collection of bouding boxes and scores for the presence of object class instances in those boxes.

Hierarchical structure of the feature map for different scale and ratio.

1. Data augmentation is crucial.
2. 

SSD is very sensitive to the bounding box size. In other words, it has much worse performance on smaller objects than bigger objects. This is not surprising because those small objects may not even have any information at the very top laryers.



## Feature Pyramid Networks for object detection ##

The construction of our pyramid involves a bottom-up pathway, a top-down pathway, and lateral connections

Is it true that the hierarchy of the network gives the power of different scale?
