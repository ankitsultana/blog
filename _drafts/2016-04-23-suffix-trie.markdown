---
title: Suffix Trie
layout: post
tags: [algorithms]
---

Motivation Problem:

> Given an empty string $$S$$, there will be $$Q < 10^3$$ queries, of two types. Type $$1$$ will be
> to append a given character to the string. Type $$2$$ will ask for the $$k$$ th lexicographical
> substring. Type $$3$$ will ask for the number of distinct substrings.

---

### List of operations that can be performed using suffix trie

$$n$$ is size of the string

1. $$k^{th}$$ lexicographical suffix in $$O(n)$$ blah.

2. Check if a given string $$p$$ is a substring of original string in $$O(\|p\|)$$.

3. Longest Common Prefix of two suffixes in $$O(log_{2}(n))$$

4. Number of distinct substrings in $$O(1)$$
