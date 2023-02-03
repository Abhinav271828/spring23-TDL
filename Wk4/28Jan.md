---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 28 January, Saturday (Lecture 7)
author: Taught by Prof. Charu Sharma
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Graph Neural Networks
## Motivation
Consider how we could give a graph as input to a deep neural network. We cannot use an ordinary FFN with the adjacency matrix and node feature matrix – this will only work for graphs of a certain size.

We know that CNNs proceed by manipulating a smaller square of pixels in a larger image. Following the same idea, we can work with neighbourhoods in a general graph.

Thus, we generate node embeddings based on local network neighbourhoods. Each node combines information from its neighbours through an *aggregation function* – this is the main characteristic of a graph convolutional network. The neighbourhood around each node defines a computational graph.  
More specifically, nodes have embeddings at each layer, and the embeddings at the $k^\text{th}$ layer are informed by nodes that are $k$ hops away.

## Aggregation Functions
The simplest aggregation functions are mean pooling and passing the messages through a trainable neural network.

One common function is
$$h_v^{(k+1)} = \sigma\left(W_k\sum_{u\in N(v)} \frac{h_u^{(k)}}{|\mathcal{N}(v)|} + B_kh_v^{(k)}\right)$$
This is simply a linear layer (followed by an activation) on the average of the neighbours' embeddings and the node's own embedding at the previous layer.  
Note that the trainable parameters are specific to a layer.

This method is permutation equivariant.

## Matrix Formulation
The above equation can be implemented efficiently by sparse matrix operations. The summation expression can be represented as
$$D^{-1}AH^{(k)},$$
where $D$ is a diagonal matrix with the degrees of the nodes and $A$ is the adjacency matrix.

Thus the complete equation is
$$H^{(k+1)} = \sigma(D^{-1}AH^{(k)}W_k^T + H^{(k)}B_k^T).$$

## Loss Function
We can find the loss of the model by, for example, comparing the inner products it produces to some pre-defined similarity function:
$$\mathcal{L} = \sum_{u, v}\text{CE}(y(u,v), \langle z_u, z_v \rangle).$$