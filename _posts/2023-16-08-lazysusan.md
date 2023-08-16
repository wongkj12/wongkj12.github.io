---
layout: post
title: "The Lazy Susan puzzle"
date: 2023-08-16 00:10:00+0800
description: An interesting puzzle on a Lazy Susan
tags: math
categories: notes
related_posts: false
---

Here is an interesting problem I encountered a long while ago:

> A genie arranges $$2^n$$ coins in a circle on a Lazy Susan. They are randomly oriented, and you are blindfolded so that you cannot tell whether a coin is facing heads or tails. A round consists of you flipping any number of the coins in front of you. If all coins are facing the same direction (i.e all heads or all tails), then the game ends. Otherwise, the genie then rotates the Lazy Susan by a *random* angle, and the next round begins. Devise an algorithm to be able to end the game in a finite number of rounds.

It was quite surprising that a solution even exists, considering that we have so little information!

Here is an example of solving a game in 7 rounds when $$n=2$$. We can represent the coins as a string of '1's and '0's (heads or tails), and we can also represent a flip action as a string of '1's and '0's, where a '1' at position k indicates that we flip the coin at position k.

```
0010
1000 (flip 1010)
0001 (genie rotates by 3 clockwise)
1101 (flip 1100)
0111 (genie rotates by 2 clockwise)
1101 (flip 1010)
1110 (genie rotates by 1 clockwise)
0110 (flip 1000)
0110 (genie rotates by 0 clockwise)
1100 (flip 1010)
0110 (genie rotates by 1 clockwise)
1010 (flip 1100)
0101 (genie rotates by 1 clockwise)
1111 (flip 1010 END)
```

The sequence of moves shown above is in fact a deterministic solution for n = 2. Any n = 2 game will terminate within these 7 rounds! If we name the moves $$A=1010$$, $$B=1100$$, $$C=1000$$, the solution is the pattern $$ABACABA$$. In general, the solution for arbitrary n can be shown inductively to be the following:

*Suppose the sequence of moves $$s_1,s_2,\ldots,s_k$$ is a solution for $$2^{n-1}$$ coins. Then let $$m_i = s_i\cdot s_i$$ (concatenation of $$s_i$$ to itself), and $$m_i' = s_i\cdot 00\ldots 00$$ (concatenation of $$s_i$$ to $$2^{n-1}$$ zeroes). Let the move $$d = 11\ldots 1100\ldots 00$$ ($$2^{n-1}$$ ones followed by $$2^{n-1}$$ zeroes), and define the sequence $$S=(m_1,m_2,\ldots,m_k)$$. Then the sequence $$S,d,S,m_1',S,d,S,m_2',S,d,S,m_3',\ldots,m_k',S,d,S$$ is a solution for $$2^n$$ coins.*

**Proof:**

The solution boils down to the two rough ideas:

1. If a configuration for $$2^n$$ coins is symmetrical, then we can apply the solution for $$2^{n-1}$$ coins symmetrically (we do this whenever we apply S every other move).

2. Otherwise, we apply a move in S "asymmetrically" to make the configuration closer to symmetry. (i.e. we apply the moves $$m_i'$$ in between every "S, d, S").

The addition of the moves 'd' will be explained in (2).

For (1):

Consider the symmetrical configuration 11001100. Rotated by 1 clockwise, it becomes 01100110. This is the same as rotating "1100" by 1 clockwise to "0110", then concatenating it to itself. In other words, symmetry is always maintained after rotation, and is equivalent to rotating each symmetric half seperately. (To prove this more formally, consider any symmetric configuration $$a_1a_2\ldots a_ka_1a_2\ldots a_k$$. After rotation by 1 clockwise, it becomes $$a_ka_1a_2\ldots a_{k-1}a_ka_1a_2\ldots a_{k-1}$$, which is $$a_ka_1a_2\ldots a_{k-1}$$ concatenated to itself, i.e. the rotation acts symmetrically. For any arbitrary rotation by k, we can then continue inductively.)

Thus for symmetrical configurations in $$2^n$$ coins, it is equivalent to solving for $$2^{n-1}$$ coins symmetrically. 

For (2):

What if the configuration is not symmetrical, and how can we make it symmetrical? For any given configuration $$L\cdot R$$ (where $$L$$ and $$R$$ are the left and right halves of $$2^{n-1}$$ coins respectively), we can think about the string $$Q = L \oplus R$$ (where $$\oplus$$ is the XOR operation). For example, given the configuration $$11001010$$, $$Q=1100\oplus 1010 = 0110$$. On the other hand, if a configuration is already symmetric, then $$Q=L\oplus R = L\oplus L = 00\ldots00$$. If we rotate $$11001010$$ by 1 clockwise to $$01100101$$, then $$Q$$ becomes $$0011$$ - in other words, $$Q$$ is also rotated by 1 clockwise. In general, whenever a rotation is applied to a configuration, $$Q$$ is also rotated by the same amount! (Can be proven formally in a similar manner as in (1))

Next, notice that applying a flip "asymmetrically" allows us to change $$Q$$ accordingly. For example, given the configuration $$01001100, Q=1000$$, after applying the flip $$1000\cdot 0000$$, $$Q$$ becomes $$0000$$. This was equivalent to applying the "flip" $$1000$$ to $$Q$$.

Now, if a configuration is not symmetrical, there are 2 cases to consider: $$Q=11\ldots 11$$ and $$Q\neq 11\ldots 11$$. If $$Q=11\ldots 11$$, then we can simply apply the flip $$d=11\ldots 1100\ldots 00$$ to make $$Q=00\ldots 00$$.

If $$Q \neq 11\ldots 11$$, then making $$Q=00\ldots 00$$ is equivalent to solving the game in $$2^{n-1}$$ coins, thus we apply the sequence of flips asymmetrically!

Finally, note that whenever we apply the symmetrical moves $$S$$, $$Q$$ is invariant (up to rotations). Hence the sequence $$S,d,S,m_1',S,d,S,m_2',S,d,S,m_3',\ldots,m_k',S,d,S$$ must solve the game, for a maximum of $$2^{2^{n-1}}-1$$ rounds.

---

We could take advantage of symmetry because the number of coins, $$N$$, was a power of two. However, what about other values of $$N$$? **It turns out that only tables with $$N=2^n$$ coins can be solved deterministically!**

**Proof**:

First, we show that no tables where $$N$$ is odd can be solved deterministically.

Take $$N=9$$, and consider a periodic configuration like $$100100100$$. Since we are blindfolded, we never know which exact configurations the coins can be in, only what they may rotate to. Thus we only look at all possible rotations of $$100100100$$, i.e. the *orbit* $$\{100100100,010010010,001001001\}$$ ("orbit" as per group theory). This orbit has size 3 since $$100100100$$ is periodic under rotation with cycle length 3. For odd $$N$$, aside from the solved orbits $$\{00\ldots 00\}$$ and $$\{11\ldots 11\}$$, all orbits have size $$>2$$ since 2 does not divide $$N$$ and thus a configuration cannot be periodic with cycle length 2. However, each flip can only solve at most 2 configurations at once (e.g. the flip 10011 solves configurations 10011 and 01100) - in _any_ orbit with size $$>2$$, there will be a nonzero probability of failure. Thus the number of rounds played can be arbitrarily large, and odd tables cannot be solved deterministically.

Next, we show that having a solution for $$N$$ coins implies there is a solution for $$N/2$$ coins. 

Solving the $$N$$ coin case means we are able to bring any asymmetric configuration in $$N$$ coins to a symmetric one. In other words, we can make the quantity $$Q=L-R$$ zero, which is equivalent to the $$N/2$$ coin problem.

Combining the above two facts, we can see that only tables of size $$2^n$$ may be solved deterministically.

