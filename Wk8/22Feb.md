---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 22 February, Wednesday (Lecture 12)
author: Taught by Prof. Charu Sharma
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Relational GCN
## Heterogeneous Graphs
In many applications of graphs, we have nodes or edges of different types; *e.g.*, in knowledge graphs. A relational GCN, or RGCN, allows us to model this.

## Architecture
A relation GCN differs from a GCN in that it parameterises the weights by the type of the node. Thus the message is
$$m_{u,r} = \frac1{c_{u,r}}W_rh_u.$$
This is summed over $u \in \mathcal{N}(v)$ and $r$ to obtain the message passed to $h_v^{(l+1)}$.

However, this idea suffers from a lack of scalability. We address this by constraining the weight matrices to be sparse (generally block-dimensional).

Another practice is *basis learning*, where we share weights across different relations. We express each $W_r$ as a linear combination of basis transformations.