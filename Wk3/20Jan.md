---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 20 January, Friday (Lecture 5)
author: Taught by Prof. Charu Sharma
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

The *centrality* of a node is is defined recursively as
$$c_v = \frac1\lambda \sum_{u\in\mathcal{N}(v)c_u}.$$
We solve this by using the eigenvalues of the adjacency matrix $A$ – if $c$ is an eigenvector of $A$ with eigenvalue $\lambda$, then $c$ satisfies the above equation.  
We usually use the highest eigenvalue of $A$ (and the corresponding eigenvector) for centrality.

Another definition of centrality relies on the *betweenness* of a node:
$$c_v = \sum_{s, t \neq v} \frac{|\{\text{shortest paths between } s \text{ and } t \text{ containing } v\}|}{|\{\text{shortest paths between } s \text{ and } t\}|};$$
and yet another on its *closeness*:
$$c_v = \frac1{\sum_{u \neq v} \text{shortest path length between } u \text{ and } v}.$$

The *clustering coefficient* of a node $v$ is defined as
$$e_v = \frac{|\{(v_1, v_2) \in \mathcal{E}: v_1, v_2 \in \mathcal{N}(v)\}|}{k_v \choose 2}.$$
The clustering coefficient of a node $u$ counts the number of triangles around $u$.