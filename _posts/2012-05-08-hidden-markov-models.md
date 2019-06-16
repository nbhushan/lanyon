---
layout: post
title: Hidden Markov models
categories: algorithms
---


### Stochastic Processes and discrete time Markov chains

A stochastic process is said to have the Markov property if the
conditional probability of future states depends only on the present
state and is independent of the past states. Consider a first order
discrete time Markov model with a sequence of random variables . At any
given instant of time, $$z_{n}$$ can take values from a discrete set
<span>1,2,.,K</span> where is the number of states. In the first order
discrete case, we can formalize the Markov property as:

$$P(z_{n}=j|z_{n-1}=i,z_{n-2}=k,...)= P(z_{n}=j|z_{n-1}=i)
\label{eq:markovproperty}$$

Furthermore, the transition probability $$P(z_{n}=j|z_{n-1}=i)$$ is assumed to be time-homogeneous i.e the transition probabilities are independent of
time. This property leads to a set of transition probabilities
$a_{ij}=P(z_{n}=j|z_{n-1}=i)$$ defined as:

$$a_{ij}(n) = a_{ij} ~~\forall n$$

The transition probabilities in a time homogeneous Markov chain are
determined by a transition matrix A.

$$a_{ij} = P(z_{n}=j|z_{n-1}=i)~~;~~~~ 1\le i \le K, ~1\le j \le K$$

The rows of A form different probability mass functions over the states and each row is governed by a multinomial distribution. The transition matric $A$ is also called a stochastic matrix and A satisfies the following
constraints:

$$a_{ij}~\ge~0$$

$$\sum_{j=1}^{K}a_{ij}~=~1$$

A time homogeneous Markov chain is stationary only when the following
condition is satisfied:

$$P(z_{1}=k) = P(z_{1+h}=k)=P(z_{n}=k) ~~\forall k$$

All stationary Markov chains are time homogeneous, but the inverse is
not true. To prove this, consider a stationary process defined by
$$P(z_{n}=k)= P(z_{n-1}=k)$$, this gives us

$$\begin{split}
a_{ij}(n) &= \frac{P(z_{n}=i, z_{n-1}=j)}{P(z_{n-1}=j)}\\
a_{ij}(n+\tau) &= \frac{P(z_{n+\tau}=i, z_{n+\tau-1}=j)}{P(z_{n+\tau-1}=j)}\\
a_{ij}(n) &= a_{ij}(n+\tau)
\end{split}$$

Hidden Markov Models {#hidden-markov-models}
--------------------

In the previous section, the topic of Markov models was considered,
where each state corresponded to an observable event. When the
observation becomes a probabilistic function of the state, the resulting
model becomes a doubly embedded stochastic process. The underlying
stochastic state sequence is now hidden, but can be inferred through
another set of observable stochastic process (sequence of
observations)as shown in Figure  [fig:standardHMM].

### Parameter set of an Hidden Markov Model

A HMM is a tuple , where $$\lambda (\pi,A,B)$$ can be formalized using the
parameters $$~\pi,~A~and~ B$$. We now proceed to describe the elements of
n HMM.

#### State transition probability distribution $$A$$, whose entries are defined as

$$a_{ij} = P(z_{n}=j|z_{n-1}=i)~~;~~~~ 1\le i \le K, ~1\le j \le K$$

and having constraints

$$a_{ij}~\ge~0$$

$$\sum_{j=1}^{K}a_{ij}~=~1$$

#### Initial state distribution $$\pi$$

$$\pi_{k} = P(z_{1}=k)~~;~~~~ 1\le k \le K$$

$$\sum_{k=1}^{K}\pi_{k}~=~1$$

#### Observation probability distribution, also known an emission model, $$B$$ is defined as the probability of generating an observation *$$y_{n}$$* from state *$$z_{n}=k$$*. This is almost always a parametrized distribution.

$$B_{k}(y_{n}) = P(y_{n}|z_{n}=k)~~,~~ 1\le k\le K$$

### HMM as a generative model

The HMM models the joint distribution of the states(outputs) and the
observations (inputs). By sampling from this distribution it is possible
to generate synthetic data points in the input space. Given the number
of states K and a HMM $$\lambda=(\pi,A,B)$$ we can use the model as a
generator to output an observations sequence $$Y_{1:N}$$ of N observations
where

$$Y_{1:N} = y_{1},y_{2},y_{3},..,y_{N}$$

The 3 problems solved by a HMM
------------------------------

A hmm model $$\lambda=(\pi,A,B)$$ can be used to solve three problems of
interest that are useful in real world applications. They are:

Problem 1
:   <span> Given an observation sequence Y and a model
    $$\lambda=(\pi,A,B)$$, What is the probability of the data, i.e
    $$P(Y;\lambda)$$? </span>

Problem 2
:   <span> Given an observation sequence Y and a model
    $$\lambda=(\pi,A,B)$$, what is the state sequence that is most likely
    to have generated the observation sequence ? </span>

Problem 3
:   <span> What are the parameters $A,~B~and~\pi$ of the model
    $$\lambda=(\pi,A,B)$$ that maximize the likelihood of observing a data
    sequence $$P(Y;\lambda)$$? </span>

To understand more about a hidden Markov model solves these problems, readers are guided to Chris Bishop's <a href="https://www.microsoft.com/en-us/research/people/cmbishop/#!prml-book" target="_blank">PRML</a> textbook.
