---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 04 March, Saturday (Lecture 14)
author: Taught by Prof. Makarand Tapaswi
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Attention (contd.)

# Theory of GNNs
Supposing we start with all nodes sharing the same feature, how well can a GNN distinguish different graph structures?

We know that different local neighbourhoods define different computational graphs. These computational graphs are rooted subtrees around each node.  
Subtrees of the same depth can be recursively characterised from the leaf nodes to the root nodes.  
GNNs can distinguish nodes with different subtree neighbourhoods if every step of its neighbour aggregation is injective. Thus injective aggregation functions lead to the most expressive GNNs.

Note also that neighbour aggregation can be characterised as a function over a multiset. In practice, an MLP is a good option for this – this is implemented in *graph isomorphism networks* (GINs) – since they can learn to be injective. Thus, theoretically, GINs are the most powerful kind of GNN.

# Graph Isomorphism Networks
In the original GIN model, the aggregation function is modelled as
$$\begin{split}
\text{GINConv}\left(c^{(k)}(v), \left\{c^{(k)}(u)\right\}_{u \in \mathcal{N}(v)}\right) = \text{MLP}_\phi[(1+\epsilon)&\text{MLP}_f\left(c^{(k)}(v)\right) \\
+ \sum_{u \in \mathcal{N}(v)}&\text{MLP}_f\left(c^{(k)}(u)\right)]
\end{split}$$

Because of the injectivity constraint (which we expect the GIN to learn), the MLP eventually models a hash function. Thus GINs can be shown to be as powerful as a WL kernel.