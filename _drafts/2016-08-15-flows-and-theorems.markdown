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

> **Theorem 2:** For a given network with integral capacities, there always
> exists a maximum flow such that flow pushed along every edge is an integer.

**Proof:**

Omitted as available online

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

> **Problem 5:** Given a bipartite graph, where each node has some associated weight, find
>                the minimum vertex cover.

**Solution:**

Build a graph, with one partite on left side, and the other on the right side.

Add an edge between every edge on the left and every edge on the right, with capacity equal
to the associated weight of the node on the left side.

Similarly, add an edge between every node on the right side and the sink, with capacity equal
to the associated weigth of the node on the right side.

Now for every edge in the original graph, add an edge from the left to the right, with
an infinite capacity.

Now consider any path which goes from source - some node of left side - some node of right side - sink.

Now let's see what does minimum cut mean.

We need to disconnect source and sink, so we can either of the following three edges:

First say the sink is $$s$$, sink is $$t$$ and the node on the left is $$l$$ and the one on the right
is $$r$$

1. $$(s, l)$$
2. $$(l, r)$$
3. $$(r, t)$$

We will definitely not cut edge 2, because that has infinite capacity.

So we will either cut 1 or 3.

Here is the key idea:

Cutting edge 1 means that $$l$$ is in $$VC_{min}$$

Cutting edge 3 means that $$r$$ is in $$VC_{min}$$

Note that not cutting edge 2 means that at least one of $$l$$ or $$r$$ must be in $$VC_{min}$$

And cutting exactly one of 1 or 3 means that exactly one of $$l$$ or $$r$$ must be in $$VC_{min}$$

Since for every node $$l$$ on the left, there is exactly one edge connecting $$(s, l)$$, implies
that we will include every node on the left exactly once (if we cut $$(s, l)$$) in $$VC_{min}$$.

Same argument can be given for the nodes on the right.

Now let's confirm that such a cut and the resulting the set of vertices is in fact a vertex cover.

Assume that there exists a edge $$E$$ between some $$l$$ and $$r$$ such that $$E$$ is not covered.

Then, both of the edges, $$(s, l)$$ and $$(r, t)$$ must *NOT* be cut.

But then there exists a path between $$s$$ and $$t$$, which is a contradiction to our definition
of an $$S$$ $$T$$ cut.

---

> **Problem 6:** Given a partially ordered set, find minimum size of partition or maximum anti chain

**Solution:**

Note that sizes of both of these will be the same by Dilworth's theorem.

I highly recommend that you try and figure out how to find the minimum partition or maximum anti chain
on your own.

The key observation is that every matching corresponds to a partition. And size of a partition is

$$

|V| - |M|

$$

For an input DAG $$G(V, E)$$, create a graph with a left partite consisting of vertices from $$V$$ and
create an identical right partite. For every edge $$(a, b)$$, add an edge from $$a$$ in the left
partite to $$b$$ in the right partite.

Add edges from source to all vertices in the left partite, and similarly for vertices in the right partite
and the sink. All capacities should be 1.

The maximum anti chain consists of all elements that are not present in the minimum vertex cover.

To understand this, realize that the complement of a vertex cover in the modified graph will represent
an anti chain.

Note that you can also add weights to vertices, and the arguments will still hold.

---

> **Problem 7:** Given a DAG such that every vertex has a positive weight,
> find a subset $$S$$ of vertices with maximum weight such that for any edge $$(u, v)$$, the following holds
> $$u \in S \implies v \in S$$.

**Solution:**

This problem is also known as [Maximum Weight Closure](https://en.wikipedia.org/wiki/Closure_problem#Reduction_to_maximum_flow) Problem.
To understand how to create the graph, refer wikipedia.
