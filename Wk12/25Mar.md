---
title: Topics in Deep Learning (CS7.602)
subtitle: |
          | Spring 2023, IIIT Hyderabad
          | 25 March, Saturday (Lecture 17)
author: Taught by Prof. Makarand Tapaswi
header-includes:
- \newfontfamily\devanagarifont{KohinoorDevanagari-Regular}
---

# Probabilistic Graphical Models
Probabilistic graphical models represent probability distributions; they encode the independence structure of a set of variables with a graph. They allow us to use graph algorithms for inference and learning.

In a PGM, each variable is represented as a node and dependencies are represented as edges.

## Independence
Each variable is conditionally independent of its non-descendents given its parents.  
For any node, the *Markov blanket* is defined as the set of its parents, children and children's parents. A node is then independent of any other variable given its Markov blanket.

## Markov Models

### Hidden Markov Models