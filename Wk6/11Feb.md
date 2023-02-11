---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 11 February, Saturday (Lecture 10)
author: Taught by Prof. Charu Sharma
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# GNNs (contd.)
## Training
### Negative Sampling
During training, it is inefficient to train over *all* pairs of nodes; instead, we sample $k$ "negative" (non-adjacent) nodes for each adjacent node, and train over this dataset. We sample nodes with probability proportional to their degree in order to pick as many "hard" negatives as possible.

### Random Walks
We generally train by defining adjacency as co-occurrence on a random walk (which can be efficiently approximated by negative sampling). Many strategies for random walks are possible, which will affect the node embeddings learnt.  
Node2vec is one method to learn node embeddings, which uses a biased 2$^\text{nd}$-order random walk to define adjacency. It is defined by parameters that trade off between local and global views – in a sense, between BFS and DFS. These parameters are:

* the *return parameter* $p$, which defines the likelihood of returning to the previous node
* the *walk-away parameter* $q$, which defines the likelihood of moving further away from the previous node

We assign $\frac1p$ to the previous node, and $\frac1q$ to each of the nodes further away from the previous node than the current node (?). We normalise these values to sample the next node in the walk.  
Thus, a low value of $p$ corresponds to a more BFS-like walk, while a low value of $q$ corresponds to a more DFS-like walk.

# Graph Embeddings
One possible way to embed a graph is to average the embeddings of all its nodes.

Another approach is to add a virtual node to represent the graph (typically a subgraph) and run a standard node embedding algorithm.

A third approach involves anonymous walks – walks which identify nodes only by the timestep at which they first appeared in the walk, and not by their actual name. We then represent graphs as probability distributions over walks of $l$ steps. To lower-bound the error in the distribution by $\varepsilon$ with probability less than $\delta$, we need to sample
$$m = \left\lceil \frac2{\varepsilon^2}(\log(2^\eta-2)-\log\delta)\right\rceil$$
anonymous walks.

This leads us to another idea: learn embeddings for (anonymous) *walks*, and use them to generate graph embeddings. We learn to predict walks that co-occur within a $\Delta$-sized window. The embedding for the graph is learnt simultaneously with those of the walks.