---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 15 February, Wednesday (Lecture 11)
author: Taught by Prof. Charu Sharma
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Page Rank
The idea behind this approach is simple – each in-link is considered to "vote" for the page it leads to.  
Each link's vote is proportional to the importance of its source page – if page $i$ has importance $r_i$ and has $d_i$ out-links, each gets $\frac{r_i}{d_i}$ votes.  
The importance of a page is the sum of the votes of its in-links.

We cannot solve this system by using methods like Gaussian elimination, as the number of nodes may get prohibitively large. Instead, we consider a matrix formulation of the problem, for which we define a *stochastic outdegree matrix*
$$M_{ji} = \mathbb{1}(i \to j) \frac1{d_i}.$$
Now if $r$ is the importance vector, with the constraint that
$$\sum_i r_i = 1,$$
we have that
$$r = M \cdot r.$$
Thus $r$ is an eigenvector of $M$ with eigenvalue 1. This can be interpreted as a stationary distribution for a random walk following a transition matrix $M$ – thus we can compute it in a similar way, by simulating a random walk and finding the fixpoint of the operation $(M \cdot)$ (power iteration).

The problems with page rank are:

* "Spider traps" (nodes with only incoming and self-edges) absorb all the importance.
* Some pages are dead ends, which causes importance to "leak out".

We solve the spider trap issue by defining a parameter $\beta$ – the probability that a random walk does *not* jump to a random page. Thus the walk "teleports" out of a spider trap in a few steps.  
Similarly, we allow the walk to reach a random page if it is at a dead end. However, this means that the matrix is not column stochastic anymore – we resolve this by *always* teleporting when there is nowhere else to go.

The final formulation is
$$r_j = \sum_{i\to j} \beta \frac{r_i}{d_i} + (1-\beta)\frac1N,$$
which is the PageRank equation described by Brin and Page in 1998 for Google. Using this formulation, $r$ becomes an eigenvector of the matrix
$$G = \beta M + (1-\beta) \left[\frac1N\right]_{N \times N}.$$

# Matrix Factorisation and Node Embeddings
## Adjacency
One simple way to connect node embeddings to matrix factorisation is to define $u, v$ as being similar if they have an edge between them, which means we want
$$Z^TZ = A.$$
This is generally not solvable exactly, but it is possible to optimise $\argmin_Z ||A - Z^TZ||_2$.

## Co-Occurrence
We may also define similarity as co-occurrence in a random walk. The matrix-factorisation formulation of this notion is more complex, but it is possible; see [this paper](https://arxiv.org/abs/1710.02971)[^1] for more details.

However, random walk-based node embeddings do not capture structural similarity (since two nodes being structurally similar does not mean that a random walk will include both of them).

[^1]: Qiu, Jiezhong, et al. "Network embedding as matrix factorization: Unifying deepwalk, line, pte, and node2vec." *Proceedings of the eleventh ACM international conference on web search and data mining.* 2018.