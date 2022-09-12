[文章链接](https://github.com/weslynn/AlphaTree-graphic-deep-neural-network/tree/master/GNN图神经网络)

challenges

1. Irregular structures of graphs.
2. Heterogeneity and diversity of graphs.
3. Large-scale graphs.

tasks

1. Node-focused tasks: node classification, link prediction, node recommendation, etc.
2. Graph-focused tasks: graph classification, estimating various graph properities, generating graphs, etc.

Graph Recurrent Neural Networks

Node-level RNNs

idea: encode graph structural information, each node $v_i$ is represented by a low-dimensional state vector $s_i$.

Graph-level RNNs

idea: a single RNN is applied to the entire graph to encode the graph states.

Graph Convolutional Networks

spectral convolutions: perform convolution by transforming node representations into the spectral domain using the graph Fourier transform or its extensions.

spatial convolutions, which perform convolution by considering node neighborhoods.

Graph Autoencoders



要想对图进行学习，首先需要对图的顶点数据，边数据和子图数据进行降维处理，也就是graph embedding。