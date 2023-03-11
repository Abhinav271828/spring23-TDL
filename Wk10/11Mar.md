---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 11 March, Saturday (Lecture 15)
author: Taught by Prof. Charu Sharma
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Knowledge Graphs
A knowledge graph is a heterogeneous graph that captures entities (nodes), types and relationships (edges).

Knowledge graphs are commonly huge – they have millions of nodes and edges – and incomplete. Many true edges are missing from it.

Processing such knowledge bases (using GNNs) has some advantages over other types of KBs – GNNs encode topology, do not require feature engineering, and are inductive. Traditional methods, however, are also less expensive and simpler.

A simpler form of the link-prediction task is the *tail-prediction* task – given a subject and a relation, we must predict the object.

## KG Representation
Edges in KGs are represented as triples $(h, r, t)$. For the tail-prediction task, we want to model the entities and relations such that the embedding of $(h, r)$ is close to that of $t$.

One method, TransE, uses the scoring function $f_r(h,t) = -||h+r-t||$. Note that it can then model antisymmetric and compositional relations, but not symmetric or one-to-many relations.

TransR is another method that models each relation as a vector $r$ with a *projection* $M_r \in \mathbb{R}^{k \times d}$. Now the scoring function is $f_r(h,t) = -||M_rh + r - M_rt||$.  
TransR can model symmetric, antisymmetric, one-to-many, inverse and compositional relations.

We also have DistMult, which uses the scoring function $\langle h, r, t \rangle$. It can be viewed as the cosine similarity between $h \otimes r$ and $t$, where $\otimes$ represents the Hadamard product.  
This method can model one-to-many and symmetric relations, but not antisymmetric, inverse or compositional relations.

ComplEx models entities and relations in $\mathbb{C}^k$ instead of $\mathbb{R}^k$. The scoring function is $\langle h, r, \overline{t} \rangle$. This can model antisymmetric, symmetric, inverse and one-to-many relations, but not compositional relations.