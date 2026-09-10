---
layout: post
title: "The crossing lemma and unit distance points"
date: 2024-05-25 00:03:00+0800
description: 
tags: math
categories: notes
related_posts: false
---

I came across a proof of the "crossing lemma": a neat result on the crossing number of graphs, and an application of the probabilistic method.

The **crossing number** $$\operatorname{cr}(G)$$ of a graph $$G$$ is the smallest number of crossings over all possible plane drawings of $$G$$. Despite its simple description, apparently not much is known about $$\operatorname{cr}(G)$$. Even the crossing number of $$K_n$$ remains unknown! 

**Crossing lemma:** For any graph $$G=(V,E)$$ with $$\vert E\vert\geq 4\vert V\vert,$$ we have $$\operatorname{cr}(G)\geq \frac{\vert E\vert^3}{64\vert V\vert^2}.$$

**Proof:** First we show a simpler lower bound $$\operatorname{cr}(G)\geq \vert E\vert - 3\vert V\vert$$. To see this, we use the well-known fact that if $$G$$ is planar, then $$\vert E\vert \leq 3\vert V\vert -6$$ (can be proven by double-counting the edges over each face and applying Euler's formula). Then given any minimal-crossing plane drawing of $$G,$$ we can remove exactly $$\operatorname{cr}(G)$$ edges to obtain a planar graph. Thus $$\vert E\vert - \operatorname{cr}(G)\leq 3\vert V\vert - 6,$$ so $$\operatorname{cr}(G)\geq \vert E\vert - 3\vert V\vert + 6 \geq \vert E\vert - 3\vert V\vert.$$

Let $$m=\vert E\vert, n=\vert V\vert$$. Now consider such a plane drawing of $$G$$ with $$t=\operatorname{cr}(G)$$ crossings. Let $$H$$ be an induced subgraph of $$G$$ obtained by sampling each vertex with probability $$p$$. In expectation, $$H$$ has $$pn$$ vertices, $$p^2 m$$ edges and $$p^4 t$$ crossings (since each crossing is uniquely formed from exactly $$2$$ edges which requires sampling $$4$$ particular vertices). Now, taking expectations over the previous bound, we have $$p^4 t\geq p^2m - 3pn \implies t\geq \frac{m}{p^2} - \frac{3n}{p^3}.$$ Since $$\vert E\vert \geq 4\vert V\vert,$$ we can set $$p=\frac{4n}{m}\leq 1$$ to obtain $$t\geq\frac{m^3}{64n^2}.$$

It is particularly useful in deducing nontrivial bounds of the size of some combinatorial structures. For example this interesting result from discrete geometry:

**(Szeméredi-Trotter)** Let $$P$$ be a set of $$n$$ points in the plane, and let $$L$$ be a set of $$m$$ straight lines on the plane. The number of pairs $$p\in P$$ and $$l\in L$$ such that $$p\in l$$ is at most $$O(m^{2/3}n^{2/3}+m+n)$$.

We are trying to maximise the number of incidences between points and lines, so we may assume that each $$l\in L$$ contains at least one points $$p\in P.$$ Let $$t$$ be the number of such incidences. Then consider the graph $$G=(P,E)$$ where an edge is between two points if they are consecutive points on some line $$l\in L$$ (i.e. the straight-line graph induced by the drawing of $$P$$ and $$L$$).  We can see that $$G$$ has $$n$$ vertices and $$t-m$$ edges (consider the number of edges each line contributes wrt the incidences). Then, any crossing in $$G$$ must be formed from $$2$$ lines in $$L$$. If $$\vert E\vert = t-m \geq 4n = 4\vert P\vert,$$ then we have

<center>$${m\choose 2}\geq \operatorname{cr}(G) \geq \frac{(t-m)^3}{64n^2}$$.</center>
by the crossing lemma which implies $$t\in O(m^{2/3}n^{2/3}+m).$$ Otherwise, $$t-m < 4n$$, which implies $$t\in O(m+n).$$ In any case, $$t\in O(m^{2/3}n^{2/3}+m+n).$$

With the above we can also prove strange things like this:

**Claim:** For any three sets $$A,B,$$ and $$C$$ of $$s$$ real numbers, $$\vert A\cdot B + C\vert = \vert\{ab+c:a\in A,b\in B,c\in C\}\vert\in\Omega(s^{3/2}).$$

Reference: 
[https://ti.inf.ethz.ch/ew/courses/Geo20/lecture/gca20-3.pdf](https://ti.inf.ethz.ch/ew/courses/Geo20/lecture/gca20-3.pdf)

CS5330 23/24 course notes