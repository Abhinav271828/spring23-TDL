---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 25 January, Wednesday (Lecture 6)
author: Taught by Prof. Charu Sharma
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

Link-level features:

* Distance-based: uses shortest path length
* Local neighbourhood overlap: captures how many neighbours are shared
* Global neighbourhood overlap: uses global graph structure

# Kernel Methods
A kernel is a function that measures similarity between two data points (*e.g.* graphs), using an inner product on some feature representation. Two common graph kernels are the graphlet kernel and the Weisfeiler-Lehman kernel.

The graphlet feature vector is defined as follows. For a graph $G$ and a list of graphlets $\mathcal{G}_k = (g_1, \dots, g_{n_k})$,
$$(f_G)_i = |\{g_i : g_i \subseteq G\}|, i \in \{1, \dots, n_k\}.$$
However, this representation is expensive to compute, since the subgraph isomorphism test is NP-hard. We cannot do better than $\mathcal{O}(nd^{k-1})$, where $d$ is the maximum degree of the graph.

Weisfeiler-Lehman is a more efficient representation. It is developed iteratively – we start by assigning a colour $c^{(0)}(v)$ to each node, and then iteratively refine them by
$$c^{(k+1)}(v) = \text{HASH}\left( \{c^{(k)}(v), \{c^{(k)}(u) : u \in \mathcal{N}(v)\}\}\right).$$
The $K^\text{th}$ iteration gives a representation that incorporates the $K$-hop neighbourhood.  
Each iteration takes time linear in the number of edges. Furthermore, the number of colours is at most the number of nodes, and only these many values need to be considered when computing the similarity.


Graph neural networks proceed in a very similar way to the updating of feature representations for the WL kernel. Each node is assigned an initial vector, whereafter the vectors are updated by combining their neighbours' embeddings at each timestep.