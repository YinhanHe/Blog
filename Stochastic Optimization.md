# Stochastic Optimization
## Brief Intro
This is a reading conclusion of **Stochastic Optimization** from Lauren A.Hannah. Stochastic optimization is optimization with randomness is present(either objective function or constraints). Main division is single stage problem(i.e. problems with a single time period, try to find single optimal dicision) and multistage problems(multiple time preriods, try to find an optimal sequence of decisions, such as scheduling water releases from hydroelectric plants over two year period).
## Single Stage Stochastic Optimization
This is an optimization situated at non-subsequent recourse decisions. Here is example:
$$\zeta^{\*}=\min_{x \in X}\{f(x) = \mathbb{E}[F(x, \xi)]\} $$
In this example, x is decision and $\xi$ is outcome(a random variable), as it is random, so we could just estimate the decision by calculating its expectation of cost function respect to each possible outcome caused by this decision and minimize it to find which is the best decision, and this is the straightforward explanition for the optimization above.
If 
1. the decision space X is convex
2. objective function $F(x, \xi)$ is convex in x for any \xi
then we could use some traditional deterministic algorithms to deal with it, but if not, then there are specialized methods
* stochastic ruler
* nested partitions
* branch and bound
* tabu search

In this part, we explore classical methods.
### Problem Consideraritions
Some assumptions on optimization problem structure.
#### Noise generation: exogenous or endogenous.
random outcome $\xi$ is exogenous if decision x does not effect distribution of $\xi$, else endogenous.
#### Data generation: constructive or black box
Observation of $F(x, \xi)$ is constructive if for given $\xi$, $F(x, \xi)$ can be evaluated for any x. But for black box, we can only generate F with specific x.
#### Data treatment: batch vs online
When we put all observations together to reach a decision, it is called batch data evaluation, if observations are suqeuentially processed, then it is called onlinedata evaluation.
### Sample Average Approximation
This uses sampling and deterministic optimization to solve problem.
1. Sampling.Instead of calculating $\mathbb{E}[F(x,\xi)]$, this can be approximated by Monte Carlo sampling in some situations.Let $(\xi_i)_{i=1}^{n}$ be a set of i.i.d. realization of $\xi$, and let $F(x, \xi_i)$ be cost function realization for $\xi_i$. So the expected cost function is approximated by average of realizations:
$$\mathbb{E}[F(x,\xi)]\approx \frac{1}{n} \Sigma_{i=1}^{n}{F(x, \xi_i)}$$
2. Search. The R.H.S. is deterministic, so deterministic optimization can be used to solve the approximated minimizer:
$$\xi_{n}^* =min_{x\in X}\{f_n(x) = \frac{1}{n}\Sigma_{i=1}^{*}F(x, \xi_i)\}$$
To guarantee convergence to global optimality, the previous two prerequisites should be satisfied.And note this method is only available for exogenous and constructive methods. 

Most theoretical results follow from the Law of Large NUmbers and Central Limit theorem. So i may repost those theorems again and the proof of those theorems are written in another blog of mine.

