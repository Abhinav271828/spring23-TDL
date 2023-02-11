---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 08 February, Wednesday (Lecture 9)
author: Taught by Prof. Makarand Tapaswi
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# GNNs
## A GNN Layer
### Message
The "message" passed between nodes at each layer is computed from each neighbour of the current node, and the node itself.
$$m_u^{(l)} = \text{Msg}\left(h_u^{(l-1)}\right) ; u \in \mathcal{N}(v) \cup \{v\}$$

### Aggregation
Each node $v$ aggregates the messages from its neighbours. This is usually done using some kind of pooling function like mean, max, or sum.  
We include a message from the node itself and combine it with the aggregated representation from the former message via concatenation or summation.
$$h_v^{(l)} = \text{Concat}\left(\text{Agg}\left(\left\{m_u^{(l)} : u \in \mathcal{N}(v)\right\}\right), m_v^{(l)}\right).$$

We may also have a nonlinearity added to either the message or the aggregation

## Other Architectures
An RNN can be considered a GNN with two nodes – one representing $X$ and one representing $H$. The message is passed from $X$ to $H$ at each step, where the aggregation is summation and $W_x$ and $W_h$ are the transformation matrices. We also have a tanh nonlinearity.

A GCN creates the message by multiplying by $D^{-1}AW^{(l)}$ and aggregates by summation. The final nonlinearity is a sigmoid.

## Over-Smoothing
GNNs run the risk of *over-smoothing* – all node embeddings converge to the same value. This is because the receptive field overlap quickly grows between two neighbours as the number of layers increases.  
In practice, this means that we avoid as far as possible increasing the number of GNN layers. We can instead make layers more expressive (by changing the aggregation/message functions to, say, MLPs), or adding pre- or post-processing layers, or adding skip connections.