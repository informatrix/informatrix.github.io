---
layout: post
title: Object Detection Basic 1
---

In computer vision area, object detection is the first step before we can do the object recognization. In this article, I will try to summarize my first knowledge about object detection techniques.


### State-of-the-art
The cascade is the most successful detection technique first appeared in 2001. The idea is quite simple. The raw pixel is not used as the features, but instead cascade is building some features based on the rectange area. Physically, it defines the feature as the first two order of gradients. The feature dimension can be very large. They applied AdaBoost to reduce the feature dimension. After that, they apply the cascade algorithm to speed up the detection procedure.

### Histogram of oriented gradient
In HOG, they have designed a new feature sets, which is based on the histogram of oriented gradient. Then apply the SVM to train the data.

### DPM
DPM is the most recent one. There are many details inside. The basic idea is to encode the object information in two levels of hierarchy. The root filter is a coarse feature map. The part model is twice the spatial resolution relative to the features captured by the root.

#### Basic model

$$
\begin{align}
f_\beta(x) & = \max_z \beta \Phi(x,z) \\
\beta &= (F_0, \ldots, F_n, d_1, \ldots, d_n, b)
\end{align}
$$

where $$\beta$$ is the concatenation of the root filter, the part filters and deformation cost weights. $$z$$ is the specification of the object, and $$z = (P_0, \ldots, p_n)$$ and $$p_i = (x_i, y_i, l_i)$$. Here we denote the model using the tuple $$(F_0, P_1, \ldots, P_n)$$ where $$F_0$$ is the root filter, and each model is defined by 3-tuple $$(F_i, v_i, d_i)$$, $$F_i$$ is the filter for the $$i$$-th part, $$v_i$$ is `anchor` position, and $$d_i$$ is a 4-dimensional coefficients of the quadratic function defining the deformation cost model. So the objective function is

$$
\text{score}(p_0, \ldots, p_n) = \sum_{i=0}^n F_i \phi(H,p_i) - \sum_{i=0}^n d_i \phi_d(d_{x_i}, d_{y_i}) + b  
$$

wphere
p
$$
(d x_i , d y_i) = (x_i, y_i) - (2(x_0,y_0) + v_i)
$$

is the displacement of the $$i$$-th part relative to its anchor position and

$$
\phi_d(dx , dy) = (dx, dy, dx^2, dy^2)
$$

are deformation features.

#### Matching
To detect the objects in the image, we compute the *score* for each root location according to best placement of parts,

$$
score(p_0) = \max_{p_1, \ldots, p_n} score(p_0, \ldots, p_n)
$$

Distance transforms (`dynamic programming`) can be used to compute the score efficiently. The computational procedure can be briefed as

$$
\begin{align}
R_{i,l}(x,y) &= F_i \phi(H, (x,y,l)) \\
D_{i,l}(x,y) &= \max_{dx,dy} (R_{i,l}(x +dx, y + dy) - d_i \phi_d(dx,dy)) \\
score(x_0,y_0, l_0) &= R_{0,l_0} + \sum_{i=1}^n D_{i,l_0 - \lambda} ( 2 (x_0, y_0) + v_i) + b
\end{align}
$$

#### Latent SVM
The model can be trained using SVM, which is

$$
L_D(\beta) = \frac{1}{2} \| \beta\|^2 + C \sum_{i=1}^n \max(0, 1- y_i f_{\beta}(x_i))
$$

We should not that the object function is not convex. However it's `semi-convex` since  it's convex for negative examples.

>If there is a single possible latent value for each positive example, then $$f_\beta(x_i)$$ is linear for a positive example and the loss due to each positive is convex, then the loss function is convex.

#### Optimization
Let $$Z_p$$ specify a latent value for each positive example, we define $$L_D(\beta, Z_p) = L_{D(Z_p)}(\beta)$$,

$$
L_D(\beta) = \min_{Z_p} L_D(\beta, Z_p)
$$

Algorithms

1. *relabel positive examples*: Optimizae $$L_D(\beta, Z_p)$$ over $$Z_p$$ by $$z_i = \arg\max_z \beta \Phi(x_i,z)$$
2. *Optimize beta*: Optimize $$L_D(\beta, Z_p)$$.

#### Data-mining hard examples
There are enormous amounts of negative examples in the database. `Hard-example` can be used to speed up the training. The idea is that we can reduce the negative examples to hard example, but keep the optimal solution unchanged. 


