---
title: Suffix Array
layout: post
tags: [algorithms]
---

### List of operations that can be performed using Suffix Arrays

$$n$$ is size of the string

1. Longest common prefix of any two suffixes of the string in $$O(log_{2}(n))$$

### Sample Problems

---

> Given a string of size $$n < 10^{5}$$, determine its minimum lexicographic
> rotation.

**Solution:** Just append the string with itself, and then create a suffix array.
For the first suffix you encounter with size $$ \ge n $$, print its first $$n$$ letters.

---

> Given a string of size $$n < 10^{5}$$, you will have to answer queries asking for
> the $$k^{th}$$ lexicographical substring of given string. There can be two
> variants of this problem, one in which distinct substrings are considered and
> the other in which all substrings are considered. Solve both of them.

**Solution:** Create an array that stores the number of distinct substrings so far
and blah blah blah
