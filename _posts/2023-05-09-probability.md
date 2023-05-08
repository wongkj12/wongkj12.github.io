---
layout: post
title: "CLRS Appendix C: Some probability and bounds (In progress)"
date: 2023-05-09 00:03:50+0800
description: Some probability and useful bounds
tags: clrs math
categories: notes
related_posts: false
---
(In progress)

An interesting problem (simulating an unbiased coin given a biased one):
> **Exercise 5.1-3 (rephrased)**
>
> Suppose you want to output 0 with probability 1/2 and 1 with probability 1/2.
> You have a biased function $$R$$ which outputs 1 with probability $$p$$, and 0 with probability
> $$1-p$$, where $$0 < p < 1$$. Give an algorithm which uses $$R$$ to output
> an unbiased answer. What is the expected running time?

Call $$R$$ twice and store the results in variables $$x$$ and $$y$$. Note that since $$x$$ and $$y$$
are independent and have the same distribution, by symmetry, $$P(x < y) = P(x > y)$$, so we just output 1 whenever
$$x > y$$, 0 if $$x < y$$, and repeat otherwise. The probability of termination in one iteration is constant, equal to
$$P(x \neq y) = 2p(1-p)$$, so the number of iterations until termination follows a geometric distribution. Thus in expectation,
the number of iterations will be $$\frac{1}{2p(1-p)}$$.

--- 

While I learn probability, here I'll list some interesting bounds/formulas from Appendix C:

**Stirling's approximation (3.18)**

$$n! = \sqrt{2\pi n}\left(\frac{n}{e}\right)^n (1+\Theta(1/n)).$$

**Binomial bounds**

$${n\choose k} = \left(\frac{n}{k}\right)\left(\frac{n-1}{k-1}\right)\cdots\left(\frac{n-k+1}{1}\right) \geq \left(\frac{n}{k}\right)^k.$$

$${n\choose k} \leq \frac{n^k}{k!} \leq \left(\frac{en}{k}\right)^k.$$

$${n\choose k} \leq \frac{n^n}{k^k (n-k)^{n-k}}.$$

**Boole's inequality/Union bound**

$$\mathbb{P}\left(\bigcup_i A_i\right) \leq \sum_i \mathbb{P}(A_i).$$

**Jensen's inequality (Probabilistic form)**

If $$X$$ is a random variable and $$f$$ is a *convex* function (i.e. for all $$x,y$$ and all $$0 \leq \lambda \leq 1$$, we have
$$f(\lambda x + (1-\lambda)y) \leq \lambda f(x) + (1-\lambda)f(y)$$), then

$$\mathbb{E}(f(X)) \geq f(\mathbb{E}(X)), $$

provided that the expectations exist and are finite.

**Markov's inequality (Exercise C.3-6)**




