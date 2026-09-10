---
layout: post
title: "CLRS Appendix C: Tails of the binomial distribution (in progress)"
date: 2023-07-12 00:23:43+0800
description: The tails of the binomial distribution
tags: clrs math
categories: notes
related_posts: false
---

The **tails** of the binomial distribution refers to the two regions of the distribution $$b(k;n,p)$$ that are far from the mean $$np$$.

First, we may provide bounds on the right tail of $$b(k;n,p)$$. Let $$X$$ be a random variable denoting the number of successes in $$n$$ Bernoulli trials with probability of success $$p$$, i.e. $$X \sim Bin(n,p)$$. Then for $$0\leq k \leq n$$,

$$
\begin{aligned}
P(X\geq k) &= \sum_{i=k}^{n} b(i;n,p) \\
&\leq {n\choose k} p^k. \\
\end{aligned}
$$

**Proof:**

Clearly, whenever at least $$k$$ trials are successes, we have $$X\geq k$$. The probability of exactly $$k$$ trials being a successes is $$p^k$$, and there are $${n\choose k}$$ possible $$k$$-subsets of such trials. However, when we sum this together to $${n\choose k}p^k$$, we are "overcounting" the probabilities here, as any $$k$$-subset of trials being successes are not neccessarily disjoint events, which gives us an upper bound. More formally, we are using the union bound here.

Similarly, we can make the same statement about the left tail of $$b(k;n,p)$$:

$$
\begin{aligned}
P(X\leq k) &= \sum_{i=0}^k b(i;n,p) \\
&\leq {n \choose {n-k}} (1-p)^{n-k} \\
&= {n \choose k}(1-p)^{n-k} \\
\end{aligned}
$$

**Proof**

By a similar union-bound argument, whenever at least $$n-k$$ trials are failures, we have $$X\leq k$$.

---
