---
layout: post
title: The EM algorithm
categories: statistics
---

The EM algorithm is beautiful.

Preliminaries
-------------

It is useful to review few topics which are a pre-requisite towards
understanding the EM algorithm.

### Random Variables

A random variable is a variable which can take on a specific value in a discrete case or a range of values in the continuous case. The likelihod of the variable taking on a particular value (or a range) is governed by a probability distribution (e.g., a Gaussian).

I use the following simplified notation while defining the likelihood of a random variable *Z* taking on a value *z*:

$$P(Z=z)= p(z)$$

### Independence and conditional independence

Two random variables *Z* and *Y* are said to be statistically
independent if and only if (iff) they satisfy the following criteria:

$$P(Z=z,Y=y) = P(Z=z)P(Y=y) ~~\forall z,y$$

using the notation we introduced earlier, this becomes:

$$p(z,y) = p(z)p(y) ~~\forall z,y$$

Similarily, wwo random variables *Z* and *Y* are said to be statisticallyindependent given *X* if and only if (iff) they satisfy the following criteria:

$$P(Z=z,Y=y|X=x) = P(Z=z|X=x)P(Y=y|X=x) ~~\forall z,y,x$$

using the notation we introduced earlier, this becomes:

$$p(z,y|x) = p(z|x)p(y|x) ~~\forall z,y,x$$


### The general EM algorithm

Given a joint distribution $$P(Y,Z;\theta)$$ over observed random
variables $$Y=Y_{1:N}$$ and latent *(hidden or unmeasured)* random variables $$Z={Z_{1:N}}$$, fit by the model with parameters $$\theta$$, the goal of the EM algorithm is to maximise the likelihood function of the observed data $$P(Y;\theta)$$ with respect to the parameters $$\theta$$.

Let's assume that Z is a discrete random variable.
The log likelihood function then is given by

$$\begin{split}
l(\theta) &= \log P(Y;\theta)\\
&= \log\sum_{Z}P(Y,Z;\theta)
\end{split}$$

Furthermore, Let $$Q$$ be some distribution over the $$Z’s$$ such that

$$\begin{split}
\sum_{Z} Q(Z) = 1 \\
Q(Z) \ge 0
\end{split}$$

The likelihod function then becomes:

$$\begin{equation}
\begin{split}
\log P(Y;\theta)&= \log\sum_{Z}P(Y,Z;\theta)\\
&= \log\sum_{Z}Q(Z)\frac{P(Y,Z;\theta)}{Q(Z)}\\
&\ge \sum_{Z}Q(Z) \log \frac{P(Y,Z;\theta)}{Q(Z)}
\end{split}
\end{equation}
\label{eq:eqjensen}$$

This is obtained as a direct application of Jensen’s inequality theorem which states that for a convex function *f*

$$E\left|f(X)\right| \ge f(E\left|X\right|)$$

Consequently, the inverse holds true for concave functions and furthermore, *log* is a concave function since $$f''(log x) = \frac{-1}{x^{2}}$$.

Hence, for concave functions

$$f(E\left|X\right|) \ge E\left|f\left(X\right)\right|$$


In the previous equation, the term

$$\sum_{Z}Q(Z) \log \frac{P(Y,Z;\theta)}{Q(Z)}$$

is the expectation of the function $$\frac{P(Y,Z;\theta)}{Q(Z)}$$
with respect to some $$Z$$ sampled from the distribution $$Q$$. Applying Jensen’s inequality, we obtain

$$f\left(E\left|X\right|\right) \ge E\left|f\left(X\right)\right|$$

$$f\left(E_z\left[\frac{P(Y,Z;\theta)}{Q(Z)}\right]\right) \ge E_z\left[f\left(\frac{P(Y,Z;\theta)}{Q(Z)}\right)\right]$$

Hence, the likelihood function as a function of Q is given by:

$$\log P(Y;\theta) \ge \sum_{Z}Q(Z) \log \frac{P(Y,Z;\theta)}{Q(Z)}$$

We now have formed a lower bound on $$l(\theta)$$.
This holds for any set of distributions Q. But, to make the lower bound tight at a particular Q, we need to replace the inequality with an equality. To satisfy this, it is sufficient that take the expectation over some constant valued variable (constant for the given Q i.e., does not depend on $Z$).

Let $$\epsilon$$ denote a constant such that

$$\frac{P(Y,Z;\theta)}{Q(Z)} = \epsilon$$

Futhermore, let

$$Q(Z) = P(Z|Y;\theta)$$

then we have

$$\begin{split}
\epsilon &= \frac{P(Y,Z;\theta)}{P(Z|Y;\theta)}\\
&= P(Y;\theta)
\end{split}$$

Hence, by setting Q to be the posterior distribution of the Zs given Y
and the model $$\theta$$, we ensure that we tighten the lower bound on the log-likelihood. This forms the E step of the EM algorithm.

Additionally, In the M step we can then find the model parameters $$\theta$$ which would maximize the Q function. These two iterative processes form the EM algorithm. Due to Jensens inequality, the EM
algorithm is proven to improve the log likelihood at every iteration and is hence guaranteed to converge to an optimal solution (albeit a local one).
