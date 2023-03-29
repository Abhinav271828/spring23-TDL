---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 29 March, Wednesday (Lecture 18)
author: Taught by Prof. Makarand Tapaswi
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Probabilistic Graphical Models (contd.)
## Undirected PGMs
Undirected PGMs are also called Markov random fields. In an MRF, the Markov blanket of a node is the set of its neighbours.

Such PGMs model joint, rather than conditional, distributions. For example, given a graph with nodes $A, B, C$, where there are edges between $(A, B)$ and $(A, C)$, a model defines a potential function $\phi$ such that
$$P(A, B, C) \propto \phi(A, B) \phi(A, C).$$

We can use *factor nodes* to model DAGs using undirected graphs.

# Belief Propagation
## Sum-Product Belief Propagation