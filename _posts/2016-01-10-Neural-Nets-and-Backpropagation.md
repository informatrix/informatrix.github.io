---
layout: post
tilte: Neural Nets and Backpropagation
---


Last week, my friend recommanded a course on compute vision to me. The course turned out to be quite interesting. It is leaded by Feifei Li, who is quite famous for her work on deep learning work. You can find the course here, [CS231n: Convolutional Neural Networks for Visual Recognition](http://cs231n.stanford.edu/).

In this article, I will mainly discuss how to do `backpropagation` in neural network and the most widely used stochastic gradient descent (`SGD`) method.

Neural Network
------
Before going into details about neural networks, we should always have a good understanding of non-linear model, which serves as the basic like $$ F = ma$$ in classic Newton's Law of motion. In 2D world, if we are doing the regression, where we believe that we can formulate the problem with a funciton, then our taget is to fit a curve into the observed data, as showed

![nonlinear-model](/image/nonlinear.png){: .center-image height="400px"}

One of most powerful regression models is called Gaussian Process. For more details, please refer to [Introduction to Gaussian Process]({% post_url 2015-12-08-Introduction-to-Gaussian-Process %}).

Nerual network is a simplfied version of Gaussian Process (`GP`). The idea is to simulate the structure of neural nets inside our brain, but with very simple mathematical function. Neural network consists of many connected units. Each unit is a small computaional operator. As we can image, we can construct very complicated function/model by stacking these units.

Neuron
=============
As the basic unit, neuron is usually designed as simple as possible. The output of neuron is the activation function of results from linear combination of inputs.

$$
y = f(Wx)
$$

![neurons](/image/neuron.png){: .center-image height="350px" width="500px"}
*credited http://www.hemming.se/gslt/LingRes/NeuralNetworks.htm.*

It is obvious that one single layer is quite limited. One follow-up idea is to have many neurons, then we come to the popular neural network.

![network](/image/network.jpg){: .center-image height="200px"}
 
Inference                                              
------
With the model build above, we need to do inference to make the model work for us. The inference is about to find the best parameter/model to fit to our data and can be generalized well to unseen data. It's the ultimate goal for all learning algorithms. If you are familiar with the concept of inference, you can skip this section. But for those without much machine learning background, it make quite a long time to train your muscle mind.

*Inference is about to form a good function, where the real parameter should locate at the minimum point
*Optmization




