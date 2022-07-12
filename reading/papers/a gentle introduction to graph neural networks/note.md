Graphs are common. Real world objects are often defined in terms of their connections to other things.

A set of objects, and the connections between them, are naturally expressed as a graph.

Graph neural networks apply in areas such as antibacterial discovery, physics simulations, fake news detection, traffic prediction and  recommendation system.



### Graph Structured Data

A graph represents the relation(edges) between a collection of entities(nodes).

- Vertex attributes
- Edge attributes and directions
- Global attributes

Attributes need to be embeded into vectors.

Datas that could be modeled as graphs:

- images

- text

- molecules

- social networks

- citation networks

- machine learning models, programming code, math equations

  variables are nodes and edges are operations that have these variables as input and output.(dataflow graph)



### Graph Relative Problems

1. graph-level: predict a single property for a whole graph.
2. node-level: predict some property for each node in a graph.
3. edge-level:  predict the property or presence of edges in a graph.



### Challenges of using Graphs in Machine Learning

machine learning models typically take rectangular or grid-like arrays as input.

graphs have up to four types of information that we will potentially want to use to make predictions: 

1. nodes
   - matrix
2. edges
   - matrix
3. global-context
   - matrix
4. connectivity
   - adjacency matrix(sparse, not permutation invariant)
   - adjacency lists(tuple(i, j))



### Graph Neural Networks

A GNN is an optimizable transformation on all attributes of the graph that preserves graph symmetries(permutation invariances).

The simplest GNN

An architecture can learn new embeddings for all graph attributes but connectivity.

This GNN uses a separate multilayer perceptron(MLP)

pooling for collecting information

1. concatenate each of embedding of items into a matrix
2. aggregate the gathered embeddings

we only use connectivity when pooling information for prediction

passing messages between parts of the graph

1. for each node, grther all the neighboring node embeddings
2. aggregate all messages
3. all pooled messages are passed through an update function, usually a learned neural network.

combine edge embedding with node(not necessarily the same size)

- learn a linear mapping from the space of edges to the space of nodes
- concatenate them together



































































