---
title: Divide and Conquer Optimization to DP
layout: post
tags: [algorithms]
---

Divide and Conquer optimization can be applied to recurrences of the following type:

$$

dp(k, i) = min_{j < i}\left\{ dp(k-1, j) + C(j+1, i) \right\}

$$

where $$C$$ is some cost function

There are two ways to check if DnC Optimization can be applied.

* Check if $$A(k, i) \le A(k, i+1)$$. Here $$A(k, i)$$ is the value of the *smallest* index $$j$$ so that,

$$

dp(k, i) = dp(k-1, j) + C(j+1, i)

$$

* Check if Quadrangle Inequality exists so that:

$$

C(a, b) + C(c, d) \le C(a, c) + C(b, d)

$$

> If DnC can be applied, both of these are true. If any of these are true, then DnC can be applied

The key of the algorithm is that, if DnC can be applied, then:

$$

A(k, i) \le A(k, i+1)

$$

So, say we have to compute $$dp(i, j)$$ for all $$(i, j)$$ such that:

$$

1 \le i \le 10 \ and 1 \le j \le 200

$$

If we calculate $$dp(i, 100)$$, then we will know that for each $$1 \le j \lt 100$$, $$A(i, j) \le 100$$.

Similarly for each $$100 \le j \le 200$$, we have $$A(i, j) \ge 100$$. So we can come up with the following
pseudocode:

{% highlight cpp %}
void compute(int curr_i, int l, int r, int dyn_l, int dyn_r) {
    if(dyn_l == dyn_r) {
        // Compute for each dp(curr_i, j) for l <= j <= r
        return ;
    }
    int mid = (l + r) / 2;
    // Compute for dp(curr_i, mid) by searching in range [dyn_l, dyn_r]
    // Say A(curr_i, mid) = x
    compute(curr_i, l, mid - 1, dyn_l, x);
    compute(curr_i, mid + 1, r, x, dyn_r);
}
{% endhighlight %}

---

**Problems:** [Ciel and Gondolas \| CF](http://codeforces.com/problemset/problem/321/E),
              [Levels and Regions \| CF](http://codeforces.com/problemset/problem/673/E),
              [Guardians of the Lunatics \| HR](https://www.hackerrank.com/contests/ioi-2014-practice-contest-2/challenges/guardians-lunatics-ioi14)
