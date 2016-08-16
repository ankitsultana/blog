---
title: Flows and Theorems
layout: post
tags: [algorithms]
---

This draft is a dump of all my learning of flows:

---

> **Theorem 1:** Take any independent set of a graph, it's complement is a vertex cover

**Proof:**

Assume the theorem is not true, i.e, there exists some set $$I$$ such that $$I'$$ is
not a vertex cover. Now if $$I'$$ is not a vertex cover, then there must exist some
edge $$(a, b)$$ such that both $$a, b \in I'$$. Hence, we get a contradiction.

---

> **Theorem 2:** Size of Maximum Independent Set $$I_{max}$$ and size of the minimum
>                vertex cover $$VC_{min}$$ are related as (where $$V$$ is the set of
>                vertices)

$$

|I_{max}| + |VC_{min}| = |V|

$$

**Proof:**

Can be proven using theorem 1.

---

> **Problem 1:** Given a bipartite graph $$G(V, E)$$, how to find the size of minimum
>                vertex cover?

**Solution:**

Let's call the two partites of the graph $$P_1$$ and $$P_2$$. Connect all vertices
in $$P_1$$ to a newly created node, called $$S$$, with edges oriented from $$S$$ to
a vertex of $$P_1$$, where each edge's capacity is 1.

Similarly connect all nodes of $$P_2$$ to a newly created node $$T$$, where the edges
are oriented from some node of $$P_2$$ to $$T$$, keeping edge's capacity as 1.

Now add the edges from $$E$$, and orient them from some node in $$P_1$$ to some node
in $$P_2$$, again keeping edge weight equal to 1.

The maximum flow in this graph is equal to the minimum vertex cover.

Try to think why that is the case.

---

> **Problem 2:** Find the number of edges in maximum matching of a bipartite graph

**Solution:**

We use [Konig's Theorem](https://en.wikipedia.org/wiki/K%C5%91nig%27s_theorem_(graph_theory))
without proof, which states the following:

> In a bipartite graph, number of edges in a maximum matching is equal to the number of vertices
> in the minimum vertex cover

Now the problem is the same as **Problem 1**

We will prove an easier theorem:

---

> **Theorem 3:** Prove that the number of vertices in the minimum vertex cover is at least the number
>                of edges in maximum matching.

**Proof:**

I will omit the proof, for brevity of the post, and just share the key idea, which is that to
cover all edges of $$M$$, you will need at least $$|M|$$ vertices.

---

**Definition:** Henceforth, I will call a vertex matched if it is incident to at least one vertex
                which is in $$M$$

> **Theorem 4:** Given a graph $$G(V, E)$$, and a matching $$M$$, then $$VC_{min}$$ contains only
>                matched vertices.

**Intuition:**

We can use Konig's Theorem to understand this. Since

$$

|VC_{min}| = |M|

$$

and each edge of $$M$$ has to be covered, we have to take at least one vertex for each edge $$E$$
that belongs to $$M$$

Because of Konig's Theorem, we will have to take *exactly 1 vertex from each matched edge*.

Now if we have to take $$k$$ more vertices for our minimum vertex cover, then size of $$VC_{min}$$
will become greater than $$|M|$$

---

> **Problem 3:** Given a bipartite graph, find all the edges that belong to some maximum matching
>                $$M$$

**Solution:**

TODO

---

> **Problem 4:** Find the *vertices* of any minimum vertex cover. In other words, for any
>                minimum vertex cover $$VC_{min}$$, you have to find all vertices $$v$$
>                such that $$v \in VC_{min}$$

**Solution:**

First observation is that because of **Theorem 4**, if any matched node is connected to an unmatched
node, then that matched node has to be in our $$|VC_{min}|$$.

Second observation is that for each matched edge, exactly one of the vertices involved will be
in $$|VC_{min}|$$.

If you have understood the above two observations, then I think you will be able to understand
the following algorithm:

1. Arrange the graph, so one of the partite is on the left, and the other is on the right

2. Orient the matched edges so that they point from right to left, and orient the unmatched
   edges so that they point from left to right.

3. For every unmatched vertex on the left, start traveling along the newly oriented edges.

4. Elements of $$|VC_{min}|$$ are the unvisited matched vertices on the left, and the matched
   vertices on the right.

Visited matched vertices on the right since they were visited by an unmatched vertex, hence
to cover the edge from we came to the matched vertex, we need to take the matched vertex
in our $$|VC_{min}|$$.

Similarly we take unvisited vertices on the left because their matched vertex on the right
was not taken, so to cover their matched edge, we take the unvisited vertex on the left.

---
