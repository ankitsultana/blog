---
title: Weighted gcd Sum
layout: post
tags: [math, algorithms]
---

Consider there is a function

$$

w(k, n)

$$

such that we have to find the sum:

$$

S = \sum_{i=1}^n w(i, n) * gcd(i, n)

$$

The sum above is equal to:

$$

S = \sum_{d|n}{\left(\phi(d) \sum_{j=1}^{n/d}{w(dj, n)}\right)}

$$

**Problem:** [HackerEarth May Easy 2016](https://www.hackerearth.com/may-easy-16/algorithm/super-functions/description/)

Essentially you have to find two types of sum, where the corresponding $$w$$ is:

$$

w(i, n) = n^i

$$

and

$$

w(i, n) = 2^i

$$

**Note:** The third type of sum can be written in terms of the first type, that is left as an exercise to the reader
