---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 25 February, Saturday (Lecture 13)
author: Taught by Prof. Charu Sharma
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Attention
We have seen that typical message passing happens in the following way
$$h_v^{(l)} = \sigma\left(\sum_{u \in \mathcal{N}(v)} \alpha_{uv}W^{(l)}h_u^{(l-1)}\right).$$
$\alpha$ is a weighting factor – it quantifies the importance of node $u$'s message to node $v$. It is defined explicitly based on the structural properties of the graph.

Clearly, $\alpha$ must be a (possibly parameterised) function of $h_u$ and $h_v$. For example, we could set
$$\alpha_{uv} = \operatorname*{softmax}_{u \in \mathcal{N}(v)}(h_u^T h_v).$$
We may also use temperature-scaled softmax to control the flatness of the distribution.  
More typically, however, we use projections of the representations into different spaces for the dot product, *i.e.*,
$$\alpha_{uv} = \operatorname*{softmax}_{u \in \mathcal{N}(v)} \left((W_uh_u)^T (W_vh_v)\right).$$