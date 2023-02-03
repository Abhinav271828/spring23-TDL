# Embeddings

Map nodes into an embeddings space 

Similar embeddings between nodes imply similarity in the node. 

Two nodes far away may be
- structurally 
- semantically


Assume we have a graph $G$

- $V$ is the vertex set 
- $A$ is the adjacency matrix 

Goal is to encode nodes so that similarity in the embedding space is meaningful (say dot product)

we want to optimize like so

$$
\text{similarity}(u, v) \sim z_v ^T z_u
$$

Note that we only have an adjacency matrix rn

## "Shallow" Encoding 

Encoder is just an embedding-lookup 

Each node is assigned a unique embedding vector

how do we define node similarity?

perhaps if they are linked 
perhaps if they have shared neighbours 
perhave if they have similar "structural roles"

suppose the first one was our goal, then the loss would look something like

$$
\sum _{u, v} || z_u ^T z_v - A  _{u, v}||
$$


We will now learn node similarity definition that uses random walks

This is a self supervised way of learning node embeddings
- We are not utilizing node lables
- we are not utilizing node features

essentially the embeddings represent structure exclusively

embeddings are task independent


The idea is: starting at a given node, what is the probability that some other node comes in a random walk

$$
z_u ^T z_v \sim \text{probability that }u \text{ and } v \text{cooccur on a random walk over a graph}
$$

