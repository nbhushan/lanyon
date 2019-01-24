---
layout: post
title: Hidden markov models
categories: statistics
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

The transition probability $$P(z_{n}=j|z_{n-1}=i)$$$ is assumed to be
time-homogeneous i.e the transition probabilities are independent of
time. This property leads to a set of transition probabilities
$a_{ij}=P(z_{n}=j|z_{n-1}=i)$$ defined as:

$$a_{ij}(n) = a_{ij} ~~\forall n$$

The transition probabilities in a time homogeneous Markov chain are
determined by a transition matrix A.

$$a_{ij} = P(z_{n}=j|z_{n-1}=i)~~;~~~~ 1\le i \le K, ~1\le j \le K$$

The rows of A form different probability mass functions over the states.
A is also called a stochastic matrix and A satisfies the following
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

[-\>,\>=stealth’,shorten \>=1.5pt,auto,node distance=2.0cm, semithick]

​(A) <span>$z_0$</span>; (B) [right of=A] <span>$z_1$</span>; (C) [right
of=B] <span>$z_2$</span>; (qdots) [right of =C] <span>$\cdots$</span>;
(D) [right of=qdots] <span>$z_N$</span>;
=[fill=blue!10,draw=black,thick,text=black,scale=1] (H) [below of=B]
<span>$y_1$</span>; (I) [below of=C] <span>$y_2$</span>; (J) [below
of=D] <span>$y_N$</span>;

​(A) edge (B); (B) edge (C); (C) edge (qdots); (qdots) edge (D); (B)
edge (H); (C) edge (I); (D) edge (J);

[fig:standardHMM]

### Parameter set of an Hidden Markov Model

A HMM is a tuple , where $$\lambda (\pi,A,B)$$ can be formalized using the
parameters $$~\pi,~A~and~ B$$. We now proceed to describe the elements of
n HMM.

State transition probability distribution, A
:   = {}, where

    $$a_{ij} = P(z_{t}=j|z_{t-1}=i)~~;~~ 1\le i,j \le K$$

    and having constraints

    $$a_{ij}~\ge~0$$

    $$\sum_{j=1}^{K}a_{ij}~=~1$$

Initial state distribution,
:   = {$\pi_{k}$} where

    $$\pi_{k} = P(z_{1}=k)~~,~1\le k \le K$$

    $$\sum_{k=1}^{K}\pi_{k}~=~1$$

Observation probability distribution,
:   Also known an emission model, B is defined as the probability of
    generating an observation *$$y_{n}$$* from state *$$z_{n}=k$$*. This is
    a parametrized distribution

    $$B_{k}(y_{n}) = P(y_{n}|z_{n}=k)~~,~~ 1\le k\le K$$

### HMM as a generative model

The HMM models the joint distribution of the states(outputs) and the
observations (inputs). By sampling from this distribution it is possible
to generate synthetic data points in the input space. Given the number
of states K and a HMM $$\lambda=(\pi,A,B)$$ we can use the model as a
generator to output an observations sequence $$Y_{1:N}$$ of N observations
where

$$Y_{1:N} = y_{1},y_{2},y_{3},..,y_{N}$$

The model can be used to generate sequences as shown in
algorithm [alg:hmm~g~enerator].

[t] [alg:hmm~g~enerator]

[1] Initialize; N = Length of one sequence of observations\
Set, n=1. Choose an initial state $z_{n}$ according the the initial
state distribution $\pi$\
Generate an observation $y_{n}$ from state $z_{n}$ based on the emission
distribution $B_{n}(z_{n})$\
Transition to a new state $z_{n+1}$ based on the state transition
distribution for state $z_{n}$ If n $\le $ N, set n=n+1; return to step
2. Else terminate

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

### Computing the probability of an observed sequence

Given an observations sequence Y = $$y_{1},y_{2},...,y_{N}$$ and a model
$$\lambda=(\pi,A,B)$$, the marginal likelihood is defined as
$$P(Y;\lambda)$$. Since the state sequence is latent, to compute the
probability of an observed sequence, we need to enumerate the complete
data likelihood distribution over all possible state sequences $$\vec{Z}$$
. Marginalizing over $\vec{Z}$ and applying the chain rule, we obtain:

$$\begin{split}
P(Y|\lambda) &= \sum_{\vec{Z}}P(Y,\vec{Z};\lambda)\\
& = \sum_{\vec{Z}}P(Y|\vec{Z},\lambda)\cdot P(\vec{Z};\lambda)
\end{split}$$

We can use the conditional independence properties of a HMM to solve
$$P(Y,\vec{Z}|\lambda)$$. And we can solve $$P(\vec{Z}|\lambda)$$ as it is a
Markov chain. Hence, the above equation, can be simplified further

$$\begin{split}
P(Y;\lambda) &= \sum_{\vec{Z}}P(Y|\vec{Z},\lambda) P(\vec{Z};\lambda)\\
&=\sum_{\vec{Z}}(\prod_{n=1}^{N}P(y_{n}|z_{n},\lambda))(\prod_{n=1}^{N}P(z_{n}|z_{n-1},\lambda))\\
& = \sum_{\vec{Z}} \pi_{z_{1}}\prod_{n=1}^{N}B_{z_{n}}(y_{n})\prod_{n=2}^{N}A_{z_{n-1}z_{n}}
\end{split}$$

Using the above equation, it is possible to compute the likelihood. But
as $$z_{n}$$ can take values 1..K, the evaluation of the above sum will
take $$\Big.O(K^{N})$$ operations. Even for reasonably small values of
N=1000 and K=3, the computation is of the order of $3^{1000}$ additions
and 2000 multiplications. Hence, a more efficient method is used to
compute the likelihood. This method is called the forward-backward
algorithm which is described in detail in the next section.

#### Forward-Backward Algorithm

Consider the forward variable which defines the joint probability of the
partial observation sequence $$Y_{1:n}$ and state $z_{n}=k$$ at time *n*.

$$\alpha_{n}(k) = P(y_{1},y_{2},...,y_{n},z_{n}=k ; \lambda) ~~~1\le k \le K$$

The probability of observing the sequence $Y_{1:n}$ can be obtained by
marginalizing over the latent state variable $z_{n}$. This distribution
be factorized as shown using the Markov independence properties and the
properties of d-separation. Henceforth, the explicit dependence
displayed on (not a conditional probability) on the model $\lambda$ is
assumed to be implicit because these will remain fixed.

[t] [alg: standardforward]

[1] **Base case :** $$\alpha_{1}(k)= \pi_{z_{1}=k}B_{k}(y_{1})$$\
**Induction:**\
 $$\alpha_{n}(k)=B_{k}(y_{n})\sum_{i=1}^{K}a_{ik}~ \alpha_{n-1}(i)$$
**Likelihood:**  $$P(Y_{1:N};\lambda) = \sum_{k=1}^{K}\alpha_{N}(k)$$

$$\begin{split}
\alpha_{n}(k) &= P(y_{1},y_{2},...,y_{n},z_{n}=k)\\
&=\sum_{z_{n-1}=1}^{K}P(y_{1},y_{2},...,y_{n},z_{n-1},z_{n}=k)\\
&=\sum_{z_{n-1}=1}^{K}P(y_{n}|z_{n-1},z_{n}=k,y_{1:n-1})~P(z_{n}=k|z_{n-1},y_{1:n-1})
~ P(z_{n-1},y_{1:n-1})\\
&=\sum_{z_{n-1}=1}^{K}P(y_{n}|z_{n}=k)~ P(z_{n}=k|z_{n-1})~ P(z_{n-1},y_{1:n-1})\\
&=\sum_{z_{n-1}=1}^{K}B_{k}(y_{n})~ A_{z_{n-1}z_{n}=k}~ \alpha_{n-1}(k)\\
&=B_{k}(y_{n})\sum_{i=1}^{K}a_{ik}~ \alpha_{n-1}(i)
\end{split}$$

The forward algorithm is summarized in algorithm  [alg:
standardforward]. This algorithm is based on the Dynamic Programming
approach @Bellman1957. As shown in figure  [fig:standardalpha], at each
discrete time n, all possible state sequences will merge into the K
nodes on the lattice. Hence the computation of $$\alpha_{n}(k)$$ would
only involve the previous K values of $$\alpha_{n-1}(i)$$, where
i=1,2,..K.


The **Backward variable** is defined as:

$$\beta_{n}(k)  = P(y_{n+1},y_{n+2},..,y_{N}|z_{n}=k,\lambda) ~;~1 \le k \le K$$

Similar to the method followed to solve $$\alpha_{n}(k)$$, we marginalize
the above equation over the possible values of $$z_{n+1}$$ and use the
Markov independence properties.

$$\begin{split}
\beta_{n}(k) &= P(y_{n+1},y_{n+2},..,y_{N}|z_{n}=k)\\
&=\sum_{z_{n+1}=1}^{K}P(y_{n+1:N},z_{n+1}|z_{n}=k)\\
&=\sum_{z_{n+1}=1}^{K}P(y_{n+2:N}|z_{n+1},z_{n}=k,y_{n+1})~P(y_{n+1}|z_{n+1},z_{n}=k)~
P(z_{n+1}|z_{n}=k)\\
&=\sum_{z_{n+1}=1}^{K}P(y_{n+2:N}|z_{n+1})~P(y_{n+1}|z_{n+1})~P(z_{n+1}|z_{n}=k)\\
&=\sum_{i=1}^{K}\beta_{n+1}(i)~B_{i}(y_{n+1})~a_{ki}
\end{split}$$


[t] [alg: standardbackward]

[1] **Base case :** $$\beta_{N}(z_{N})$$= 1\
**Induction:**\
 $$\beta_{n}(k)=\sum_{i=1}^{K}\beta_{n+1}(i)~B_{n+1}(i)~a_{ki}$$

Both, the forward and backward variables require of the order of
$$O(K^{2}N)$$ computations. The likelihood of observing a given sequence
$$y_{1:N}$$ can be defined as:

$$\begin{split}
P(y_{1:N}) &= \sum_{z_{n}=1}^{K}P(y_{1:N},z_{n})\\
&= \sum_{z_{n}=1}^{K}P(y_{1:n},y_{n+1:N},z_{n})\\
&= \sum_{z_{n}=1}^{K}P(y_{n+1:N}|z_{n},y_{1:n})P(z_{n},y_{1:n})\\
&= \sum_{z_{n}=1}^{K}P(y_{n+1:N}|z_{n})P(z_{n},y_{1:n}) \\
&= \sum_{k=1}^{K} \alpha_{n}(k) \beta_{n}(k)
\end{split}$$

The above relation is obtained using the property of d-separation
@Jensen1996 in the HMM Bayesian network. We can further simplify the
expression. In order to evaluate the likelihood function, we need to run
the forward algorithm for the given sequence, and then evaluate the
value for n = N, making use of the fact that $$\beta_{N}(z_{N})$$ is a
vector of 1’s. We obtain:

$$P(y_{1:N}) = \sum_{k=1}^{K}\alpha_{N}(k)$$

### Decoding the state sequence

Finding the state sequence that best defines the data can be described
as an optimization problem. Here we wish to find the optimal sequence of
states. However, there are several optimality criteria which are
generally application dependent. In this section we look at two commonly
used criteria.

#### Posterior state sequence decoding

This optimality criteria maximizes the individual state which is
(individually) most likely at each discrete time $n$. The posterior
distribution of state $$z_{n}=k$$ given the observation sequence Y,
denoted as $$\gamma_{n}(k)$$ can be expressed in terms of the
$$\alpha~and~\beta$$ variables as shown below:

$$\gamma_{n}(k) =P(z_{n}=k|Y)$$

$$\gamma_{n}(k) =\frac{\alpha_{n}(k)\beta_{n}(k)}{\sum_{k=1}^{K}\alpha_{n}(k)\beta_{n}(k)}$$

The normalization factor $$\sum_{k=1}^{K}\alpha_{n}(k)\beta_{n}(k)$$
ensures that $$\gamma_{n}(k)$$ is a probability measure such that

$$\sum_{k=1}^{K}\gamma_{n}(k) = 1$$

The most likely state at time $n$ is given by

$$z_{nk} = \mbox{argmax}_{k}(\gamma_{n}(k))$$

However, the sequence obtained using the individually most likely states
may not be a valid sequence as it would ignore any constraints applied
on the state transition distribution. One possible solution is to modify
the optimality criteria and set it to be the most likely pairs of states
$$(z_{n-1,z_{n}})$$ or a heuristic which is based on the application.

#### The Viterbi algorithm

The Viterbi algorithm @Forney1973 [@Viterbi1967] aims to fins the most
likely path(state sequence) for the given observation sequence Y and the
corresponding model $$\lambda$$, formally defined as

$$\mbox{argmax}_{Z} P(Z|Y;\lambda)$$

We simplify this further using Bayes rule and we obtain:

$$\mbox{argmax}_{Z} P(Z|Y;\lambda) = \mbox{argmax}_{Z} \frac{P(Z,Y;\lambda)}{\sum_{Z}P(Z,Y;\lambda)}$$

The denominator does not depend on Z, hence we obtain:

$$\mbox{argmax}_{Z} P(Z|Y;\lambda) = \mbox{argmax}_{Z}P(Z,Y;\lambda)$$

One approach towards solving the above optimization problem is to try
every possible state sequence and then select the one which maximizes
the joint probability $P(Z,Y;\lambda)$. This would require $$O(K^{N})$$
computations. Similar to the forward algorithm, the Viterbi algorithm
can be solved using a dynamic programming approach as shown in
[alg:viterbi]. A detailed overview of dynamic programming is found at
Bellman’s classic paper @Bellman1957.

[t] [alg:viterbi]

[1] **Base case :** $$\delta{1}(k)= \pi(k)~B_{1}(k) $$\
$$\omega_{1}(k)= 0$$ **Recursion:**\

$$\delta{n}(j)= \max_{i} \left(\delta{n-1}(i)a_{ij}\right)~B_{1}(j) ~~i=1,2..K$$\
$$\omega_{n}(j)= argmax_{i} \left(\delta{n-1}(i)a_{ij}\right) ~~i=1,2..K$$\
**Termination:**\
$$p = \max_{i} \left(\delta{N}(i)\right)  ~~i=1,2..K$$\
$$q^{\star}_{N}= argmax_{i} \left(\delta{N}(i)\right) ~~i=1,2..K $$\
**State sequence backtracking:**\
 $$q^{\star}_{n}= \omega_{1}(q^{\star}_{n+1})$$\

### Learning the model parameters

This is one of the most interesting problems in HMMs. Given an
observation sequence $$Y_{1:N}$$, we want to estimate the model parameters
$$\lambda~=~(\pi,A,B)$$ that best fit the observation sequences. The
likelihood function is given by:

$$P(Y_{1:N};\lambda) = \sum_{\vec{Z}}P(Y_{1:N},\vec{Z};\lambda)$$

The above equation is obtained by marginalizing over all possible latent
state sequences $$\vec{Z}$$. Consider a sequence of length N and K latent
states. If we perform the summation explicitly, then the number of terms
in the summation would results in $$K^{N}$$ i.e. the number of terms grow
exponentially with N. There is no known analytical method to find the
exact $$\lambda$$ that maximizes the likelihood. The most widely used
method is a special case of the EM algorithm known as the Baum-Welch
algorithm @Baum1970. A more detailed overview of the EM algorithm is
provided in chapter [chap:hmmplus]. The Baum-Welch algorithm defines two
variables. denotes the marginal posterior distribution of the latent
state $$z_{n}$$. denotes the joint posterior distribution of two
successive latent states.

$$\gamma_{n}(z_{n}) = P(z_{n}|Y_{1:N})$$

Applying Bayes rule and using the properties of conditional
independence, we obtain

$$\begin{split}
\gamma_{n}(z_{n}) &=\frac{P(Y_{1:N}|z_{n})P(z_{n})}{P(Y_{1:N})} \\
&= \frac{P(Y_{1:n}|z_{n})P(Y_{n+1:N}|z_{n})P(Z_{n})}{P(Y_{1:N})}\\
&=\frac{P(Y_{1:n},z_{n})P(Y_{n+1:N}|z_{n})}{P(Y_{1:N})}\\
&= \frac{\alpha_{n}(z_{n})\beta_{n}(z_{n})}{P(Y_{1:N})}
\end{split}$$

Te joint posterior distribution over succesive states is given by,

$$\xi_{n}(z_{n},z_{n+1}) = P(z_{n},z_{n+1}|Y_{1:N})$$

Similar to the previous computation, by applying Bayes rule and using
the properties of conditional independence, we obtain

$$\begin{split}
\xi_{n}(z_{n},z_{n+1}) &=\frac{P(Y_{1:N}|z_{n},z_{n+1})P(z_{n},z_{n+1})}{P(Y_{1:N})} \\
&= \frac{P(Y_{1:n}|z_{n})P(y_{n+1}|z_{n+1})P(Y_{n+2:N}|z_{n+1})P(z_{n+1}|z_{n}P(Z_{n})}{P(Y_{1:N})}\\
&= \frac{\alpha_{n}(z_{n})B_{z_{n+1}}(y_{n+1})A_{z_{n}z_{n+1}}\beta_{n+1}(z_{n+1})}{P(Y_{1:N})}
\end{split}$$

This forms the E step of the Baum-Welch algorithm. Given an initial
estimate of the model, we compute the posterior distributions. In the M
step, we try to find the model that maximizes the likelihood of the
observations. The re-estimation equations of the model parameters are:

$$\pi_{i} = \frac{\gamma(z_{1}=i)}{\sum_{i=1}^{K}\gamma(z_{1}=i)}$$

$$a_{ij} = \frac{\sum_{n=1}^{N-1}\xi_{n}\left(z_{n}=i,z_{n+1}=k\right)}
{\sum_{n=1}^{N-1}\gamma(z_{n}=i)}$$

$P(y_{n}|z_{n})$ is also maximised in a similar way. For example, in the
case of Gaussian emission models, we have
$P(y_{n}|\phi_{k})~=~N(y_{n}|\mu_{k},\Sigma_{k})$ and the MLE estimate
of the parameters are:

$$\mu_{k} = \frac{\sum_{n=1}^{N}\gamma_{n}(k) y_{n}}{\sum_{n=1}^{N}\gamma_{n}(k)}$$

$$\Sigma_{k} = \frac{\sum_{n=1}^{N}\gamma_{n}(k) (y_{n}-\mu_{k})(y_{n}-\mu_{k})\prime }{\sum_{n=1}^{N}\gamma_{n}(k)}$$

Similarly, Discrete observation distribution parameters can be obtained
as outlined by Rabiner @Rabiner1989.

#### Initialization of model parameters {#subsubsec:hmminit}

The Baum-Welch algorithm must be initialized by choosing starting values
for $$\pi$$,A and the emission model (the B parameter). This initial guess
must respect the constraints associated with their probabilistic
interpretation. E.g. the row stochastic properties of A. Also any values
set initially to zero will remain zero in subsequent updates. Improper
initial estimates will lead to the Baum-Welch algorithm getting stuck in
a local optima which could be significantly worse than the global
optima. There are no exact solutions to choosing the optimal initial
model. Various techniques include manual alignment of the data i.e.
using an expert to assign each data point to a state as described by
Nathan et al. @Nathan1996. However in most cases this is not feasible as
the state cannot be easily deduced from the data. Rabiner @Rabiner1989
stated that there it is a hard problem to find suitable initial
estimates. Random initialization of A and $$\pi$$ normally is shown to
converge to meaningful estimates in the Baum-Welch algorithm. However,
to initialize the emission model B, a more clever approach is required
especially in the case of continuous distributions.Generally, techniques
such as manual segmentation of observations into states as described in
@Nathan1996, segmental K-Means @Juang1990 and Maximum Likelihood (ML)
averaging of the segmented observations. The segmental K-Means is a
variant on the widely used K-Means algorithm. In this algorithm, the
initial model is chosen randomly and then the Viterbi algorithm is used
to decode the latent state sequences. Once these state sequences are
obtained, ML estimates are obtained in the segmented observations
(segmented on the basis of the discrete state variable). The resulting
model is then compared to the previous model on the basis of a distance
score. This process is repeated until the distance score falls below a
threshold and the algorithm is said to have converged.

Limitations of the Hidden Markov Model
--------------------------------------

In a Markov chain, the duration that a specific state *k* is active is a
random variable *D* distributed according to a geometric distribution
with parameter $$p= a_{kk}$$ , where $$a_{kk}$$ is defined as
$$P(z_{n}=k|z_{n-1}=k)$$ @Rabiner1989. D has the distribution:

$$\begin{split}
P(D=d) &= P(z_{n+1}=k, ... , z_{n+d}=k, z_{n+d+1}\neq k | z_{n}=k)\\
&= a_{kk}^{(d-1)}.(1-a_{kk}) ~~~~Where~ d~\geq~1
\end{split}$$
