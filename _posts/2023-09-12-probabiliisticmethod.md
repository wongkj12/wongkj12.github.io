---
layout: post
title: "Some examples of the probabilistic method"
date: 2023-12-09 00:03:00+0800
description: 
tags: math
categories: notes
related_posts: false
---

The probabilistic method is a pretty interesting method to prove the existence of certain objects _nonconstructively_. A simple example:

> Suppose we paint 90% of the surface of a sphere red, and the remaining 10% of it blue.
> Prove that there exists an inscribed cube with vertices on the sphere such that all of its vertices are red.

**Proof:** 

Suppose we orient an inscribed cube randomly. Let $$X_i=1,$$ if vertex $$i$$ is red, and $$X_i=0$$ otherwise. Then 
since 90% of the sphere is painted red, intuitively the probability that any arbitrary vertex is red is $$\frac{9}{10}.$$ Thus
$$E(X_i)=\frac{9}{10},$$ so the expected number of red vertices in a randomly inscribed cube is $$E\left(\sum_{i=1}^8 X_i\right) =\sum_{i=1}^8 E(X_i) = 8(\frac{9}{10}) = 7.2$$.
Since the expected value is $$>7,$$ that means that there must be _some_ inscribed cube with exactly $$8$$ red vertices!

I was pretty mind-blown when I first saw the use of this method. Although we use probability, the existence is determined for certain (though without any hint as to how to construct the object). Here's another example (from an exam I took):

> Let $$[n]=\{1,2,\ldots,n\}$$ and $$T=\{(i,j,k):i,j,k\in [n]\text{ are distinct }\}$$ be a set of $$m$$ triples. 
> We say that a permutation $$S$$ of $$[n]$$ is _consistent_ with a triple $$(i,j,k)\in T$$ iff $$S$$ is of the form $$\ldots i\ldots j\ldots k\ldots$$ \\
> For example, for $$n=4,$$ a permutation $$3,1,2,4$$ is consistent with the triple $$(3,2,4).$$ \\
> Show that there exists a permutation of $$[n]$$ consistent with at least $$\frac{m}{6}$$ triples in $$T.$$

**Proof (using probabilistic method):**

Consider generating a permutation $$S$$ of $$[n]$$ uniformly at random. For each triple $$t_i\in T$$, let $$X_i$$ be
the indicator random variable that denotes when $$S$$ is consistent with $$t_i.$$ Then $$P(X_i=1)=\frac{1}{6}$$
(Since there are $$3!=6$$ ways $$t_i$$ can be permuted, only one of which can be consistent with $$S$$.) \\
Then the expected number of consistent triples will be $$E\left(\sum_{t_i \in T}X_i\right)=\sum_{t_i\in T} E(X_i) = \frac{m}{6}.$$

Here's another proof without the probabilistic method:

**Proof (using pigeonhole principle):**

Note that each triple $$t\in T$$ is consistent with exactly $$\frac{n!}{6}$$ permutations of $$[n].$$ 
Consider each of the $$n!$$ permutations of $$[n]$$ as pigeonholes, and each triple $$t$$ having $$\frac{n!}{6}$$ pigeons
denoting the permutations $$t$$ is consistent with. Then, we have $$\frac{mn!}{6}$$ pigeons to be placed into $$n!$$ pigeonholes,
so by the Pigeonhole Principle we must have some permutation of $$[n]$$ which is consistent with at least $$\frac{m}{6}$$ triples.

I find it rare when an object corresponds to more than one "pigeon", and in fact there are some restrictions as to
where each pigeon may be placed (in this case, each of the $$\frac{n!}{6}$$ pigeons must belong to different pigeonholes by definition).
Though no matter how you arrange pigeons, the Pigeonhole Principle still works.