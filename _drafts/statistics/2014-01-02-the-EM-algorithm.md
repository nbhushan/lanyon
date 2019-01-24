---
layout: post
title: The EM algorithm
categories: statistics
---

I love the EM algorithm.

Preliminaries
-------------

It is useful to review few topics which are a pre-requisite towards
understanding the EM algorithm.

### Random Variables

A random variable can take on values in a discrete (or a range of values
in the continuous case) with a certain probability. We use the following
notation while defining a random variable *Z* which we assume can take
on a value *z*:

$$P(Z=z)= p(z)$$

### Independence and conditional independence

Two random variables *Z* and *Y* are said to be statistically
independent if and only if (iff) they satisfy the following criteria:

$$P(Z=z,Y=y) = P(Z=z)P(Y=y) ~~\forall z,y$$

using the notation we introduced earlier, this becomes:

$$p(z,y) = p(z)p(y) ~~\forall z,y$$


### The general EM algorithm

Given a joint distribution $$P(Y,Z;\theta)$$ over observed random
variables $$Y=Y_{1:N}$$ and latent random variables $$Z={Z_{1:N}}$$, fit by
the model with parameters $$\theta$$, the goal of the EM algorithm is to maximise the likelihood function of the observed data $$P(Y;\theta)$$ with respect to the parameters $$\theta$$.

The log likelihood function is given by

$$\begin{split}
l(\theta) &= \log P(Y;\theta)\\
&= \log\sum_{Z}P(Y,Z;\theta)
\end{split}$$

Let $$Q$$ be some distribution over the $$Z’s$$ such that
$$\sum_{Z} Q(Z) = 1$$
$$Q(Z) \ge 0$$

We obtain:
$$\begin{equation}
\begin{split}
\log P(Y;\theta)&= \log\sum_{Z}P(Y,Z;\theta)\\
&= \log\sum_{Z}Q(Z)\frac{P(Y,Z;\theta)}{Q(Z)}\\
&\ge \sum_{Z}Q(Z) \log \frac{P(Y,Z;\theta)}{Q(Z)}
\end{split}
\end{equation}
\label{eq:eqjensen}$$

This is obtained as a direct application of Jensen’s inequality theorem
@Jensen1906 which states that for a convex function *f*

$$E\left|f(X)\right| \ge f(E\left|X\right|)$$

The inverse holds true for concave functions and log is a concave
function since $$f''(log x) = \frac{-1}{x^{2}}$$.

In equation [eq:eqjensen], the term

$$\sum_{Z}Q(Z) \log \frac{P(Y,Z;\theta)}{Q(Z)}$$

is just the expectation of the function $$\frac{P(Y,Z;\theta)}{Q(Z)}$$
with respect to some $$Z$$ sampled from the distribution $$Q$$. Applying
Jensen’s inequality, we obtain

$$f\left(E_z\left[\frac{P(Y,Z;\theta)}{Q(Z)}\right]\right) \ge E_z\left[f\left(\frac{P(Y,Z;\theta)}{Q(Z)}\right)\right]$$

From equation [eq:eqjensen], we now form a lower bound on $$l(\theta)$$.
This holds for any set of distributions Q. But, we know that to make the
lower bound tight at a particular Q, we need to replace the inequality
in equation [eq:eqjensen] with an equality. To satisfy this, it is
sufficient that take the expectation over some constant valued random
variable (constant for the given Q i.e does not depend on $Z$). Let
$$\epsilon$$ denote a constant such that

$$\frac{P(Y,Z;\theta)}{Q(Z)} = \epsilon$$

Futhermore, let

$$Q(Z) = P(Z|Y;\theta)$$

then we have

$$\begin{split}
\epsilon &= \frac{P(Y,Z;\theta)}{P(Z|Y;\theta)}\\
&= P(Y;\theta)
\end{split}$$

Hence, by setting Q to be the posterior distribution of the Zs given Y
and the model $$\theta$$, we ensure that we tighten the lower bound on the
log-likelihood. This forms the E step of the EM algorithm. In the M step
we then find the model parameters $$\theta$$ which would maximize the Q
function given in equation [eq:eqjensen]. These two processes form the
EM algorithm which is described in algorithm [alg:emcluster]. The EM
algorithm is proven to improve the log likelihood at every iteration and
is hence guaranteed to converge @Dempster1977.
