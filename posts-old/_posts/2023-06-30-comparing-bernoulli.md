---
layout: post
title: "CLRS Appendix C: Comparing sums of Bernoulli trials"
date: 2023-06-30 00:20:48+0800
description: On comparing sums of Bernoulli trials
tags: clrs math
categories: notes
related_posts: false
---

Here is an interesting exercise on probability distributions.

> **Exercise C.4-9**
>
> Let $$X$$ be the random variable for the total number of successes in a set $$A$$ of $$n$$ Bernoulli trials, where the $$i$$th trial has a probability $$p_i$$ of success, and let $$X'$$ be the random variable for the total number of successes in a second set $$A'$$ of $$n$$ Bernoulli trials, where the $$i$$th trial has a probability $$p_i' \geq p_i$$ of success. Prove that for $$0\leq k\leq n$$,
>
> $$P(X'\geq k) \geq P(X\geq k)$$.
>
> (_Hint:_ Show how to obtain the Bernoulli trials in $$A'$$ by an experiment involving the trials of $$A$$, and use the result of Exercise C.3-7.)

---

I found this exercise interesting as the result is intuitive, but it's tricky to find a way to "compare" the distributions, as per the hint.

This is one clever solution I found online, which seems obvious in hindsight:

Consider comparing each Bernoulli trial to picking a random value $$S$$ on the unit interval. If $$S \leq p_i $$, we can call that a success in set $$A$$. If $$S \leq p_i'$$, we can call that a success in set $$A'$$. If $$S \leq p_i$$, then $$S \leq p_i'$$. Then clearly, whenever there is a success for set $$A$$, there must be a success for set $$A'$$. So $$X' \geq X$$, and $$P(X' \geq k) \geq P(X \geq k)$$.
