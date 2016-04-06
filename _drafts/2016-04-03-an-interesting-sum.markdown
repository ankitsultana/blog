---
title: An interesting sum
layout: post
tags: [math, algorithms]
---

Consider the following sum:

$$

\begin{align*}
    & S(n) = \sum_{k=1}^n \frac{1}{gcd(n, k)}
\end{align*}

$$

Calculating the sum above requires a crucial observation. Let's state it below:

> Given $$n$$ and $$g$$, **$$\phi(n/g)$$** tells the number of such numbers that have their $$gcd$$ with $$n$$ equal to $$g$$

Thus we can write the sum as:

$$

\begin{align*}
    & S(n) = \sum_{k|n} \frac{\phi(n/k)} {k}
\end{align*}

$$
