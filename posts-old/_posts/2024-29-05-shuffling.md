---
layout: post
title: "Card shuffling"
date: 2024-05-29 00:03:00+0800
description: 
tags: math
categories: notes
related_posts: false
---

How many shuffles does it take to randomise a deck of cards?

It seems to be a relatively well-known fact that it takes about 7 riffle shuffles of a deck of 52 cards in order for it to become sufficiently randomised. But how do you measure if something is "random enough"? This famed analysis was covered in the paper [Trailing the Dovetail Shuffle to its Lair](https://www.stat.berkeley.edu/~aldous/157/Papers/bayer_diaconis.pdf).

If a deck is perfectly shuffled, one would expect that any permutation of 52 cards is equally likely, i.e. the ordering of cards follows the uniform distribution. Thus after a few shuffles, we want to find out how "far" our deck is from following the uniform distribution. One way to measure the "distance" between probability distributions is via the **total variation distance** (other alternatives are possible e.g. [entropy](https://en.wikipedia.org/wiki/Entropy_(information_theory))). 

The **total variation distance** between two discrete probability distributions $$X$$ and $$Y$$ over some state space $$S$$ is given by

$$\delta(X,Y)=\frac{1}{2}\sum_{s\in S}\vert\Pr[X=s]-\Pr[Y=s]\vert.$$

Equivalently, one can show that $$\delta(X,Y)=\max_{A\subseteq S}\vert \Pr[X\in A]-\Pr[Y\in A]\vert.$$

The variation distance ranges from 0 (meaning $$X$$ and $$Y$$ are the same distribution) to 1.

#### A simplified shuffle

The original analysis of variation distance of a riffle-shuffled deck relied on the [Gilbert-Shannon-Reeds model](https://en.wikipedia.org/wiki/Gilbert%E2%80%93Shannon%E2%80%93Reeds_model) of riffle shuffle permutations, and got fairly sophisticated quick. 

However we can still analyse a much simpler, though stupid way of shuffling cards:

At each step, choose a card independently and uniformly at random and place it on the top of the deck. This constitutes one "shuffle". Intuitively, if we repeat this indefinitely, the deck should eventually be sufficiently randomised. (More formally, this process is a regular Markov chain with the uniform distribution as the unique stationary distribution). 

To see how well this works with a finite number of shuffles, we need to measure the variation distance between the distribution of our deck and the uniform distribution. Suppose the variation distance after some number of shuffles is less than $$\varepsilon.$$ Then every permutation of the cards must have probability at most 

$$\frac{1}{52!}+\varepsilon$$

In fact an even stronger bound holds - for any subset $$A\subseteq S$$, the probability that the final permutation is from $$A$$ is at most $$\pi(A)+\varepsilon.$$ Thus if we shuffle a fresh deck of cards until variation distance is less than $$\varepsilon$$, the probability that an ace remains the top card is at most $$\varepsilon$$ more than if we had a completely random deck.

#### Analysis

Here we introduce the **coupling lemma:** (A coupling of $$X$$ and $$Y$$ is a joint distribution $$W=(W_1,W_2)$$ over $$S\times S$$ such that its two marginal distributions are $$X$$ and $$Y$$, i.e. the same randomness is used to generate $$X$$ and $$Y$$.)

**Lemma:** For any coupling $$W=(X,Y)$$, we have $$\delta(X,Y)\leq \Pr[X\neq Y]$$.

Thus if we can find some coupling $$(X_t,\pi)$$ with $$\Pr[X_t\neq \pi]\leq f$$, then $$\delta(X_t,\pi)\leq f.$$

Let $$X_t$$ denote the state of our deck of $$n$$ cards (this follows a distribution of _permutations_, not of cards) after $$t$$ shuffles, given some arbitrary starting distribution $$X_0$$, and let $$Y_t$$ denote the state of a deck with $$Y_0\sim\pi$$ after $$t$$ shuffles (where $$\pi$$ is the uniform distribution). Clearly $$Y_t\sim\pi$$ for all $$t$$ (since it is a stationary distribution). Whenever we perform a shuffle, we couple $$(X_t,Y_t)$$ by selecting the same card in both decks.

Observe that if we have already selected $$k$$ new cards to shuffle to the top, then the top $$k$$ cards of $$X_t$$ and $$Y_t$$ are the same. In other words, the top $$k$$ cards of $$X_t$$ will be uniformly distributed. Thus when we have selected all $$n$$ cards at least once within $$t$$ shuffles, then $$X_t=Y_t$$ or $$X_t\sim\pi.$$ This is precisely a [coupon collector](https://en.wikipedia.org/wiki/Coupon_collector%27s_problem) process: by an application of Markov's inequality, we then know that if we perform $$fn\ln n$$ shuffles, then $$\Pr[X\neq Y]\leq f^{-1}$$. In other words, after $$t=fn \ln n $$ shuffles, $$\delta(X_t,\pi)\leq f^{-1}$$.

Referring to the original paper on riffle shuffles, $$7$$ riffle shuffles successfully reduces the total variation distance from the uniform distribution to 0.334. In order to achieve the same result ($$f^{-1}=0.334$$) with our stupid shuffle, we need at least $$\frac{1}{0.334}\cdot(52)\ln (52)\approx 615$$ shuffles! (If we bound the coupon collector process a little more carefully we can make do with $$n\ln (n/f)$$ shuffles, but we still require $$\approx 262$$ shuffles).

So don't shuffle your cards one by one.

Reference: Probability and Computing: Randomized Algorithms and Probabilistic Analysis (Mitzenmacher & Upfal)