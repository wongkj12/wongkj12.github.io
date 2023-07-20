---
layout: post
title: "CLRS 5.4: Probabilistic analysis and indicator random variables"
date: 2023-07-21 00:03:00+0800
description: More probabilistic problems
tags: clrs
categories: notes
related_posts: false
---

> **Problem 5.4-6**
>
> Suppose that $$n$$ balls are tossed into $$n$$ bins, where each toss is independent and the
> ball is equally likely to end up in any bin. What is the expected number of empty bins? What is
> the expected number of bins with exactly one ball?

---

Let our indicator random variable be $$X_i$$, the event that bin $$i$$ is empty.
$$P(X_i) = (1-\frac{1}{n})^n.$$ Then our desired expectation is

$$
E(X) = \sum_{i} E(X_i) = n(1-\frac{1}{n})^n.
$$

Similarly, let $$Y_i$$ be the indicator random variable denoting the event that bin $$i$$
has exactly one ball. $$P(Y_i) = (1-\frac{1}{n})^{n-1}$$. Then the expectation is

$$E(Y) = \sum_{i} E(Y_i) = n(1-\frac{1}{n})^{n-1}$$

Interestingly, since $$(1+\frac{x}{n})^n \approx e$$, both expectations actually
tend to the same value, $$\frac{n}{e}$$ when $$n$$ is large.

$$
$$
