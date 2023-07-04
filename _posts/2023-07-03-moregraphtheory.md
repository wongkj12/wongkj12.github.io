---
layout: post
title: "CLRS Appendix B: More graph theory, and Dirac's theorem"
date: 2023-07-04 00:23:43+0800
description: Two more graph theory problems
tags: clrs math
categories: notes
related_posts: false
---

> **Problem B-2 (c) (rephrased)**
>
> Given any graph $$G=(V,E)$$, the vertex set $$V$$ can be partitioned into two subsets $$V_1,V_2$$ such that at least half the neighbours of any $$u\in V_1$$ are in $$V_2$$, and at least half the neighbours of any $$v\in V_2$$ are in $$V_1$$.

---

Note that if all of the neighbours of any $$u\in V_1$$ are in $$V_2$$ and vice-versa, this is just a 2-coloring of the graph, and $$G$$ would be bipartite. It is kind of interesting to draw the partitioning of $$G$$ as some kind of bipartite-looking graph. In fact, I think the edges that cross from $$V_1$$ to $$V_2$$ must at least be twice the number of edges from $$V_1$$ to $$V_1$$, or $$V_2$$ to $$V_2:$$

Let the number of edges that cross $$V_1$$ to $$V_2$$ be $$E_{12}$$, the number of edges only within $$V_1$$ be $$E_1$$, and similarly define $$E_2$$. Note that $$E_1 = \frac{1}{2}((\sum_{u\in V_1}deg(u)) - E_{12})$$ (by handshaking lemma). Then

$$
\begin{aligned}
E_{12} &\geq \frac{1}{2} \sum_{u\in V_1} deg(u) \\
&\geq \frac{1}{2} E_{12} + E_1 \\
\end{aligned}
$$

Thus $$E_{12} \geq 2E_1$$, and similarly $$E_{12} \geq 2E_2$$. However, I did not find this approach useful in proving the statement.

**Proof**:

Arbitrarily try to assign vertices to either $$V_1$$ or $$V_2$$. If all vertices meet the condition, then we are done. Otherwise, pick a vertex which does not satisfy the condition, and swap the subset it belongs to such that it now satisfies the condition. Note that the number of edges crossing from $$V_1$$ to $$V_2$$ strictly increases this way. If $$\lvert E\rvert$$ is finite, then this process must terminate, resulting in the desired partition.

> **Problem B-2 (d) (rephrased, i.e. Dirac's Theorem)**
>
> Given any graph $$G=(V,E)$$, with $$n \geq 3$$ vertices, if each vertex has degree at least $$n/2$$, then $$G$$ contains a Hamiltonian cycle (A cycle which visits each vertex exactly once).

---

First, we show that a longest simple path in $$G$$ is a Hamiltonian path (A path which visits each vertex exactly once). Let such a path be $$P = (v_1,v_2,\ldots,v_k)$$. Suppose there is a vertex $$u$$ in $$G$$ that is outside of $$P$$. We proceed by showing that there is a vertex $$v_j$$ on $$P$$ that is a neighbour of $$v_k$$, such that $$v_{j+1}$$ is a neighbour of $$u$$. Since $$P$$ is a longest path, all neigbours of $$v_k$$ must be on $$P$$. Thus there at at least $$n/2$$ neighbours $$v_i$$ of $$v_k$$ on $$P$$, and we mark each of the $$n/2$$ neighbours $$v_{i+1}$$ on $$P$$. Now, since $$u$$ has at least $$n/2$$ neighbours, by the Pigeonhole Principle, it is a neighbour of at least one of these marked vertices. Thus the vertex $$v_j$$ exists, and we can construct a longer path $$(v_1,v_2,\ldots,v_j,v_k,v_{k-1},\ldots,v_{j+1},u)$$ (contradiction). Thus $$P$$ must be a Hamiltonian path.

Next, given $$P = (v_1,\ldots,v_n)$$ we can construct a Hamiltonian cycle. Using a similar argument, we can show that there exists a pair $$(v_t,v_{t+1})$$ on $$P$$ such that $$v_t$$ is a neighbour of $$v_n$$ and $$v_{t+1}$$ is a neighbour of $$v_1$$. Then we can rearrange vertices to form the cycle $$(v_1,v_2,\ldots,v_t,v_n,v_{n-1},\ldots,v_{t+1},v_1)$$.
