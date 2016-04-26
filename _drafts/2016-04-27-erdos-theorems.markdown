---
title: Erdos Theorems
layout: post
tags: [algorithms]
---

There are two theorems of Erdos that one should know for competitive programming.

### 1. Erdos Gallai Theorem

The Erdos Gallai Theorem gives a necessary and sufficient condition for a finite sequence of
natural numbers to be a degree sequence of a simple graph. The theorem goes like this

> A sequence of non negative integers $$ d_1 \ge ... \ge d_n $$ can be the degree sequence of a finite
> simple graph if and only if the following two conditions hold

$$

2 | d_1 + ... + d_n

$$

and

$$

\sum_{i=1}^k d_i \le k(k-1) + \sum_{i=k+1}^n{min(d_i, k)}

$$

holds for every $$ 1 \le k \le n $$

Problem: [Codestorm Prelims BITS Pilani Problem E](https://www.codechef.com/problems/COPR16E)

### 2. Erdos Ko Rado Theorem

> Say $$S = {1, 2, ..., n}$$ and $$A$$ is a family of distinct
> subsets of $$S$$, each with size $$r$$ and each pair of sets
> in that family has a non empty intersection.
> Then the size of $$A$$ is bounded by, given that $$n \ge 2r$$

$$

\binom{n-1}{r-1}

$$

Note that if $$ 2r > n $$ then every pair of distinct subset of size
$$r$$ will have at least one element in common.

To prove this, assume that
there exists a pair of subsets $$A$$ and $$B$$, each of size $$r$$.

Since  $$A \cap B = \phi \Rightarrow n(A \cup B) = r + r = 2r > |S|$$, which is a
contradiction.

Problem: [Insomnia 2014 Problem F](http://www.spoj.com/problems/INS14F/)
