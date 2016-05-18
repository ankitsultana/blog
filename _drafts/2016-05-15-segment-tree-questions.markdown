---
title: Questions on Segment Trees
layout: post
tags: [algorithms]
---

This is a list of some standard segment tree questions and links to corresponding problems on different OJs.

---

**Problem 1:** Given an array of $$N$$ integers, and queries of type

`l r`  Return minimum and maxmium of elements in range `l` and `r`

Queries should be $$O(log_2(n))$$

**Links:** [RPLN \| SPOJ](http://www.spoj.com/problems/RPLN/) [1082 \| LightOJ](http://lightoj.com/volume_showproblem.php?problem=1082)

---

**Problem 2:** Given an array of $$N$$ integers, and queries of type

`l r`  Return the sum of elements in range `l` and `r`

Queries should be $$O(log_2(n))$$

**Link:** [CSUMQ \| SPOJ](http://www.spoj.com/problems/CSUMQ/)

---

**Problem 3:** Given an array of $$N$$ integers, and queries of two types

`1 l r x`  Add x to all elements of range l and r


`2 l r` Return sum of all elements in range l and r

Both operations should be $$O(log_2(n))$$

*Hint:* First operation is taken care of using Lazy Propagation

**Link:** [HORRIBLE \| SPOJ](http://www.spoj.com/problems/HORRIBLE/)

---

**Problem 4:** Given an array of $$N$$ integers, and queries of type

`l r`  Output the maximum contiguous subarray sum, formally return

$$

max_{\ l \le p \le q \le r}\left(\sum_{i=p}^{q}{a_i} \right)

$$

Expected Complexity is $$O(log_2(n))$$

**Link:** [GSS1 \| SPOJ](http://www.spoj.com/problems/GSS1/)

---

**Problem 5:** Same as the previous one, but with one more type of query

`x y` Set the $$x^{th}$$ element of the array to `y`

Expected Complexity is still $$O(log_2(n))$$

**Link:** [GSS3 \| SPOJ](http://www.spoj.com/problems/GSS3/)

---

**Problem 6:** Given an array of $$N$$ integers, and queries of types

`k`  Find $$k^{th}$$ element of array if this array was sorted

`x y` Set the $$x^{th}$$ element of array to `y`

Either of complexities $$O(log_2(n))$$ or $$O(log_2^2(n))$$ will do

---

**Problem 7:** Given an array of $$N$$ integers, and queries of type

`p` Find the elements with indices $$i$$ and $$j$$ such that

$$

i = min(x \ | \ x > p \ and \ a_x < a_p)

\\

j = max(x \ | \ x < p \ and \ a_x < a_p)

$$

Expected Complexity is $$O(log_2(n))$$ per query

**Link:** [Histogram \| LightOJ](http://lightoj.com/volume_showproblem.php?problem=1083)

---

**Problem 8:** Given an array of $$N$$ integers, and queries of types

`U i x`   Set the value of $$a_i$$ to `x`

`Q x y`   Find the maximum sum $$a_i + a_j$$ where $$x \le i \le j \le y$$

**Link:** [KGSS \| SPOJ](http://spoj.com/problems/KGSS)

---

**Problem 9:** You have to maintain a dynamic set `S` with the following operations

`INSERT(S, x)`   Insert `x` in `S` if it is not already present

`DELETE(S, x)`   Delete `x` from `S`, if it exists in `S`

`K-TH(S, k)`     Return the $$k^{th}$$ smallest element in S

`COUNT(S, k)`    Count the number of elements in S with value less than `k`

All operations should be $$O(log_2(n))$$

**Link:** [ORDERSET \| SPOJ](http://spoj.com/problems/ORDERSET)

---

**Note:** I realize that some of the questions don't have Problem Links yet, I will try to add them ASAP
