---
layout: post
title: "CLRS Appendix B: Three problems on trees"
date: 2023-06-30 00:20:48+0800
description: Three tree problems from Appendix B
tags: clrs math
categories: notes
related_posts: false
---

Here are three problems on trees from Appendix B.

> **Exercise B.5-3**
>
> Show that the number of degree-2 nodes in any nonempty binary tree is 1 fewer than the number of leaves. Conclude that the number of internal nodes in a full binary tree is 1 fewer than the number of leaves.

Note that in the context of a binary tree, the "degree-2" nodes refer to nodes with exactly 2 _children_.

**Proof by strong induction**: Let the number of degree-2 nodes in any tree by $$D$$, and the number of leaves be $$L$$. Let the number of nodes in a tree be $$n$$. Clearly, $$D=L-1$$ when $$n=1$$. Suppose it is true for all trees with $$\leq n$$ nodes. Consider the root of a tree with $$n+1$$ nodes. Letting subscripts $$l$$ and $$r$$ denote the left and right subtrees, we have that

$$
\begin{aligned}
D &= D_l + D_r + 1 \\
&= (L_l + L_r - 2) + 1 \\
&= (L_l + L_r) - 1 \\
&= L - 1.
\end{aligned}
$$

In a full binary tree, all internal nodes are of degree-2.

---

> **Exercise B.5-6**
>
> Let us associate a "weight" $$w(x)=2^{-d}$$ with each leaf $$x$$ of depth $$d$$ in a binary tree $$T$$, and let $$L$$ be the set of leaves on $$T$$. Prove that $$\sum_{x\in L} w(x) \leq 1.$$ (This is known as the **Kraft inequality**.)

**Proof by strong induction**: Let the number of nodes in any tree $$T$$ be $$n$$. Clearly when $$n=1$$, $$\sum_{x\in L}w(x) = 2^0 \leq 1.$$ Suppose $$\sum_{x\in L}w(x) \leq 1 $$ for all trees with $$\leq n$$ nodes. Consider the root of a tree $$T$$ with $$n+1$$ nodes. Notice that the depth of all leaves in the left and right subtrees increase by 1 relative to the root. Similarly letting subscripts $$l$$ and $$r$$ denote the left and right subtrees, we have that

$$
\begin{aligned}
\sum_{x\in L}w(x) &= \frac{1}{2}\sum_{x\in L_l}w(x) + \frac{1}{2}\sum_{x\in L_r}w(x) \\
&\leq \frac{1}{2}(1) + \frac{1}{2}(1) \\
&\leq 1.
\end{aligned}
$$

---

> **Exercise B.5-7**
>
> Show that if $$L\geq 2$$, then every binary tree with $$L$$ leaves contains a subtree having between $$L/3$$ and $$2L/3$$ leaves, inclusive.

**Proof by contradiction**: Suppose that there is a binary tree with $$L$$ leaves, with no subtrees having between $$L/3$$ and $$2L/3$$ leaves. If $$L\geq 2$$, then the root of this tree cannot be a leaf. Take the path $$x_0 = root, x_1, \ldots , x_k$$ on the tree down to a leaf, at each step picking the child subtree with the larger number of leaves. Consider the number of leaves of the subtree rooted at each $$x_i$$. Clearly the number of leaves is a decreasing sequence, so along the path the number of leaves must decrement from $$x_i$$ with more than $$2L/3$$ leaves to $$x_{i+1}$$ with less than $$L/3$$ leaves. However, if $$x_i$$ has less than $$L/3$$ leaves, then $$x_{i+1}$$ must have had less than $$2L/3$$ leaves, a contradiction.
