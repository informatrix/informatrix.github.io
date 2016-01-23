---
layout: post
title: Positive Definite and Its Application
---

The concept of postive definite(`PD`) has puzzled me when I first saw it. It's intuitive to think about the positive number, e.g. `+5`. But what does it mean by saying a matrix is positive? And you can see a lot of positive definite or positive semi-definite(`PSD`) as the requirement for some mathematical tools. In this article, I will try to summarize what my knowledge regarding the `PD`.

## Definition

First, let's define what is `positive definite`. In linear algebra, a `symmetric real` matrix $$M$$ is said to be **positve definite** if $$\mathsf{z}^TM\mathsf{z}$$ is postive for every `non-zero` vector $$\mathsf{z}$$. It's `PSD` if can be zero. It's  What does the definition tell us? It is really important to view the `PD` in the context of real application

### Quadratic real function
I guess everyone should be familiar with quadratic real function, which can be expressed as

$$
\begin{align}
f(x, y) =& w_1 x^2 + w_2 x y + w_3 y^2  + w_4 x + w_5 y + w_6\\
=& \begin{bmatrix} x & y \end{bmatrix} \begin{bmatrix} w_1 & w_2/2 \\ w_2/2 & w_3 \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix}  + \begin{bmatrix} w_4 & w_5 \end{bmatrix} \begin{bmatrix} x \\y \end{bmatrix} + w_6 \\
=& \mathsf{z}^T M \mathsf{z} + \mathsf{b}^T\mathsf{z} + c
\end{align}
$$

The above is just a vectorized form of `quadratic function`. We can generalize it to any dimensional function. Lots of real application can be modeled using quadratic function. Often the goal is to maximize the function to get the maximal profit/gain. When we apply the gradient descent method, the second derivative ( `Hessian`) tells about the convexity or concavity.

Here $$M$$ is the `Hessian` matrix for the function $$f(x,y)$$. If we let $$M$$ be a `PD` matrix, we would know that the function is convex is the local region. With the property, we could search the local minimum using the gradient method. 

### Covariance matrix
First, let us have a quick review about the definition of covariance. It's defined as

$$
\Sigma = \mathbf{E}[ (\mathsf{X} - \mathbf{E}[\mathsf{X}]) (\mathsf{X} - \mathbf{E}[\mathsf{X}])^T ]
$$

It's straightforward to derive that

$$
\begin{align}
\mathsf{z}^T \Sigma \mathsf{z}  =& \mathbf{E}[ \mathsf{z}^T(\mathsf{X} - \mathbf{E}[\mathsf{X}]) (\mathsf{X} - \mathbf{E}[\mathsf{X}])^T \mathsf{z} ] \\
=& \mathbf{E}[ ((\mathsf{X} - \mathbf{E}[\mathsf{X}])^T\mathsf{z})^T ((\mathsf{X} - \mathbf{E}[\mathsf{X}])^T \mathsf{z} )] \\
=& \mathbf{E}[ \mathsf{y}^T \mathsf{y}]\\
\ge &  0
\end{align}
$$

`PSD` is the important property for the covariance. Every positive `PSD` matrix is the covariance matrix of some multivariate distribution.

### Conditional variance

Conditional probability or posterior distribution is often used in `Bayesian` prediciton application. For general distribution, it's not that trival to work out the posterior distribution. To get the close-form expression, we usually require conjugate pair. For example, the following table shows some common used conjugate distributions.

|-----------+-------------|
|likelihood | prior       |
|-----------|:------------|
| Normal    | Normal      |
|-----------+-------------|
|Multinomial| Dirichlet   |
|-----------+-------------|

Let us dive into multivariate normal distribution. Nowadays, `big data` application is very popular. With the big data, actually Gaussian distribution can be more useful if you remember `law of large numbers`. The multivariate Gaussian distribution is defined as

$$
p(\mathsf{z}) = \frac{1}{(2\pi)^{k/2}|\Sigma|^{1/2}}\exp\left\{ -\frac{1}{2}(\mathsf{z}-\mu)^T \Sigma^{-1} (\mathsf{z} -\mu) \right\}
$$

here $$\mathsf{z} = [\mathsf{x} \quad \mathsf{y}]^T$$ and $$\Sigma = \begin{bmatrix} \Sigma_{\mathsf{x}\mathsf{x}} &  \Sigma_{\mathsf{x}\mathsf{y}} \\  \Sigma_{\mathsf{y}\mathsf{x}} & \Sigma_{\mathsf{x}\mathsf{y}} \end{bmatrix} $$.

Imaging that $$\mathsf{x}$$ is the data we observed and $$\mathsf{y}$$ is data we would like to predict, we assume that the likelihood $$p(\mathsf{x}, \mathsf{y})$$ is a multivariate Gaussian distribution as above and $$p(\mathsf{x})$$ is another multivariate Gaussian distribution. With the conjugate property, we know that posterior distribution $$p(\mathsf{y}\shortmid \mathsf{x})$$ would also follow multivariate Gaussian distribution. The question is how to derive the expression for that posterior distribution. The trick is called `Completing the square`. I found one tutorial very useful [Completing the square](https://learnbayes.org/index.php?option=com_content&view=article&id=77:completesquare&catid=83&Itemid=479&showall=1&limitstart=). According to `Bayesian rule`, we have that

$$
p(\mathsf{y} \shortmid \mathsf{x}) = \frac{p(\mathsf{x}, \mathsf{y})}{p(\mathsf{x})}
$$

To simple the derivation, we use the `precision matrix` instead of covariance matrix, which is

$$
p\left( \begin{bmatrix} \mathsf{x} \\ \mathsf{y} \end{bmatrix} \right) = \frac{1}{(2\pi)^{k/2}|\Sigma|^{1/2}}\exp\left\{ -\frac{1}{2}\begin{bmatrix} \mathsf{x}^T - \mu_{\mathsf{x}}^T & \mathsf{y}^T - \mu_{\mathsf{y}}^T\end{bmatrix}  \begin{bmatrix} Q_{\mathsf{x}\mathsf{x}} & Q_{\mathsf{x}\mathsf{y}} \\ Q_{\mathsf{y}\mathsf{x}} & Q_{\mathsf{y}\mathsf{y}} \end{bmatrix} \begin{bmatrix} \mathsf{x} - \mu_{\mathsf{x}}  \\ \mathsf{y} - \mu_{\mathsf{y}} \end{bmatrix} \right\} 
$$

Let us forget about the constant part but only focus on the exponential part, so we have that

$$
\begin{align}
p( \mathsf{y} \shortmid \mathsf{x}) &\propto  \exp \left\{ -\frac{1}{2} \begin{bmatrix}\mathsf{x}^T - \mu_{\mathsf{x}}^T & \mathsf{y}^T - \mu_{\mathsf{y}}^T \end{bmatrix} \begin{bmatrix} Q_{\mathsf{x}\mathsf{x}} & Q_{\mathsf{x}\mathsf{y}} \\ Q_{\mathsf{y}\mathsf{x}} & Q_{\mathsf{y}\mathsf{y}} \end{bmatrix}\begin{bmatrix} \mathsf{x} - \mu_{\mathsf{x}}  \\ \mathsf{y} - \mu_{\mathsf{y}} \end{bmatrix} \right\} \\
&\propto \exp \left\{  \mathsf{x}^T Q_{\mathsf{x}\mathsf{x}} \mathsf{x} - \mathsf{b}^T x - x^T\mathsf{b}  + \mathsf{b}^T Q_{\mathsf{x}\mathsf{x}}^{-1} \mathsf{b}  \right\} \\
&\propto \exp \left\{ (x - Q_{\mathsf{x}\mathsf{x}}^{-1}b)^T Q_{\mathsf{x}\mathsf{x}} (x - Q_{\mathsf{x}\mathsf{x}}^{-1} )\right\}
\end{align}
$$

Where $$b = Q_{\mathsf{x}\mathsf{y}} \mu_{\mathsf{y}} + Q_{\mathsf{x}\mathsf{y}} (y - \mu_{\mathsf{x}})$$

We need one more tool to get the expression for conditional probability, which is matrix inverse lemma, and then we can get that

$$
\begin{align}
\mu_{\mathsf{y} \shortmid \mathsf{x}} &= \mu_{\mathsf{y}} + \Sigma_{\mathsf{y}\mathsf{x}} \Sigma_{\mathsf{x}\mathsf{x}}^{-1}(\mathsf{y} - \mu_{\mathsf{y}})  \\
\Sigma_{\mathsf{y} \shortmid \mathsf{x}} &= \Sigma_{\mathsf{y} \mathsf{y}} - \Sigma_{\mathsf{y} \mathsf{x}}\Sigma_{\mathsf{x}\mathsf{x}}^{-1} \Sigma_{\mathsf{x}\mathsf{y}}
\end{align}
$$

> Based on the following discussion, we know that the conditional covariance matrix is positive semi-definite, which makes sense since it is also another distribution.

### Matrix inverse lemma

We have the following inverse lemma for any invertible M which is

$$
M^{-1} = 
\begin{bmatrix}
A & B \\
C & D
\end{bmatrix}^{-1} =
\begin{bmatrix}
(A - B D^{-1}C)^{-1} & -(A- BD^{-1}C)^{-1} BD^{-1} \\
-D^{-1}C(A - B D^{-1}C)^{-1} & D^{-1}C(A - B D^{-1}C)^{-1}BD^{-1} + D^{-1}
\end{bmatrix}
$$

Where $$ A - B D^{-1} C$$ is called the **Schur Complement of $$D$$ in $$M$$**. One interesting property for symmetric  matrix is that

> if $$C$$ is invertible, then $$M$$ is positive semi-definite if only if Schur Complement of $$D$$ is positive semi-definite.

For detail proof, please refer to [Schur Complement](http://www.cis.upenn.edu/~jean/schur-comp.pdf). The basic idea is that

$$
M^{-1} = 
\begin{bmatrix}
A & B \\
B^T & D
\end{bmatrix}^{-1} =
\begin{bmatrix}
I & BD^{-1} \\
0 & I
\end{bmatrix}
\begin{bmatrix}
A-BD^{-1}B^T & 0 \\
0 &D 
\end{bmatrix}
\begin{bmatrix}
I & BD^{-1} \\
0 & I
\end{bmatrix}
= N T N^T
$$

Basically, We know that

> $$NTN^T \succ 0 \Leftrightarrow T \succ 0  \Leftrightarrow (D \succ 0 \wedge A - BD^{-1}B^T \succ 0) $$

We need more careful discussion in case of $$ = 0$$, which should not be a problem.

### Eivenvalue
TBA

### Summary
TBA


