---
layout: post
title: "CLRS Appendix B: A theorem on graph coloring"
date: 2023-07-03 00:01:19+0800
description: An exercise on graph coloring from Appendix B
tags: clrs math
categories: notes
related_posts: false
---

> **Problem B-1 (d)**
>
> Show that if a graph $$G$$ has $$O(V)$$ edges, then we can color $$G$$ with $$O(\sqrt{V})$$ colors.

---

Here is a proof by trying the greedy algorithm:

**Proof**:

Attempt to color the graph greedily (i.e. color an arbitrary vertex, then start coloring its neighbours, using new colors whenever needed, and so on). Whenever we need to use a new color $$n$$ on a vertex, that vertex must neccessarily have edges connecting it to vertices colored in each one of the previous $$n-1$$ colors. Everytime we use a new color, mark all of these edges. Every edge is marked at most once, and so if we end the algorithm using $$c$$ colors, at least $$1+2+\ldots+c = \frac{c(c+1)}{2}$$ edges must have been marked. Thus $$\frac{c(c+1)}{2} \leq E$$, so $$\frac{c(c+1)}{2} \in O(V)$$, and we have that $$c \in O(\sqrt{V})$$.
