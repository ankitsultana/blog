---
title: Tree and Queries
layout: post
tags: [algorithms]
---

Problems involving graphs and queries and pretty common in programming contests. Such kind of problems can be categorized as follows:

\# | Update | Query
---|--------|------
1  | Point  | Point
2  | Point  | Path
3  | Point  | Subtree
4  | Path   | Point
5  | Path   | Path
6  | Path   | Subtree
7  | Subtree| Point
8  | Subtree| Path
9  | Subtree| Subtree


We will deal with example problems for each of the above category, discussing the possible strategies that can be used to solve any of the above.

---

### 1. Point Update, Point Query

This one is trivial, and I will continue on with others.

---

### 2. Point Update, Path Query

Take a motivation problem:

> Given a tree with N nodes, where each node has some associated value, you will have two types of queries

1. Update v val: Add val to vertex v

2. Query a b: Report the sum of values on path from a to b

**Solution:** Use DFS order and store sum of values from root to node, and then use BIT

---

### 3. Point Update, Subtree Query

> Given a tree with N nodes, where each node has some associated value, you will have two types of queries

1. Update v val: Add val to vertex v

2. Query v: Report the sum of values in subtree rooted at v

**Solution:** Use DFS order. Now that the tree is flattened, the question is converted to a standard point update, range query problem, which can be solved using BIT/Segtree

---

### 4. Path Update, Point Query

> Given a tree with N nodes, where each node has some associated value, you will have two types of queries

1. Update a b val: Add val to all vertices on path from a to b

2. Query v: Report the value of vertex v

**Solution:** Unknown

---

### 5. Path Update, Path Query

---

### 6. Path Update, Subtree Query

---

### 7. Subtree Update, Point Query

> Given a tree with N nodes, where each node has some associated value, you will have two types of queries

1. Update a val: Add val to all vertices in subtree of a

2. Query v: Report the value of a particular vertex

**Solution:** Flatten the tree again, now the problem translates to range update, point query, which can again be done using Segtree/BIT

---

### 8. Subtree Update, Path Query

---

### 9. Subtree Update, Subtree Query

Just flatten the tree, then any problem translates to range update, range query
