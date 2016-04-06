---
title: LCM Extreme
layout: post
tags: [math, algorithms]
---

Consider the following sum:

$$

\begin{align*}
    & S(n) = \sum_{i=1}^n\sum_{j=i+1}^{n} {lcm (i, j)}
\end{align*}

$$

You have to answer $$ 10^5 $$ queries where in each query you will given
$$ n $$ such that:

$$ 1 \le n \le 10^6 $$

Try to think over the problem a little before reading the solution below.

---

Firstly let's try to simplify the given formula a little.

Note we can define $$ S(n) $$ recursively as:

$$

\begin{align*}
    & S(n) = S(n-1) + f(n)
\end{align*}

$$

where $$ f(n) $$ is defined as:

$$

\begin{align*}
  & f(n) = \sum_{i=1}^{n-1}{lcm(n, i)}
\end{align*}

$$

If we can pre-compute the $$ f(n) $$ array, we can compute $$ S(n) $$ in
a single loop. So let's try to do that. Now, $$ f(n) $$ can be written as:

$$

\begin{align*}
  & f(n) = \sum_{i=1}^{n-1}\frac{n*i}{gcd(n, i)} = n * \sum_{i=1}^{n-1}\frac{i}{gcd(n, i)}
\end{align*}

$$

Calculating the sum above requires a crucial observation. I will state it for now:

> Given $$n$$ and $$g$$, **$$\phi(n/g)$$** tells the number of such numbers that have their $$gcd$$ with $$n$$ equal to $$g$$

Thus we can write the sum as:

$$

\begin{align*}
    & S(n) = \sum_{k|n} \frac{\phi(n/k)} {k}
\end{align*}

$$
