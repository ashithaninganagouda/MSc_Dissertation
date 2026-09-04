# Structural Analysis of Neural Network Pruning Using Graph Theory and Graphon Models
This repository contains the source code used for the experiments presented in the MSc dissertation “Structural Analysis of Neural Network Pruning Using Graph Theory and Graphon Models.”

The project investigates the structural effects of neural network pruning using graph-theoretic measures, with experiments conducted on the MNIST and CIFAR-10 datasets.

**Overview**

The experiments examine how pruning affects:

Neural network predictive performance
Network connectivity and structural fragmentation
Algebraic connectivity
Spectral properties
Minimum node degree and structural bottlenecks
Path capacity
The relationship between pruning strategy and network structure

Two complementary experimental programmes are included:

MNIST: An initial investigation using unmatched architectures and standard global magnitude pruning.
CIFAR-10: A revised investigation using approximately parameter-matched architectures and degree-constrained, connectivity-preserving pruning.


**MNIST Experiments**

The MNIST experiments use fully-connected multilayer perceptrons with the following architectures:

Balanced: 784 → 256 → 256 → 10
FrontLoaded: 784 → 512 → 128 → 10
BackLoaded: 784 → 128 → 512 → 10

The networks were trained for 10 epochs using Adam and cross-entropy loss, with three independent random seeds.

Standard global magnitude pruning was then applied at:

0%, 20%, 40%, 60%, 80%, 90%

Unlike the CIFAR-10 experiments, MNIST pruning does not explicitly preserve neuron connectivity. This allows the effects of network fragmentation caused by pruning to be examined directly.

The MNIST analysis includes:

Test accuracy
Largest connected component
Number of connected components
Spectral radius
Algebraic connectivity
Additional investigations of network capacity, node importance and weight behaviour

**CIFAR-10 Experiments**

The revised CIFAR-10 experiments use fully-connected MLPs with the structure:

3072 → h1 → h2 → 10

Three approximately parameter-matched architectures are investigated:

Architecture	h1	h2	Parameters
Balanced	256	256	855,050
FrontLoaded	270	90	855,010
BackLoaded	180	1,581	855,121

The networks were trained for 25 epochs using Adam with a cosine-annealing learning-rate schedule. Light training-time data augmentation was applied. Five independent random seeds were used for the main pruning comparison.

**Connectivity-Preserving Pruning**

The CIFAR-10 experiments implement a degree-constrained pruning procedure.

For each candidate connection, the algorithm checks whether removing the connection would cause a hidden or output neuron to lose all required incoming or outgoing connections. If so, the connection is retained; otherwise, it can be removed.

Two pruning criteria are compared:

Magnitude pruning: connections are considered for removal in ascending order of absolute weight magnitude.
Random pruning: connections are considered in random order while subject to the same connectivity constraint.

The pruning levels are:

0%, 20%, 40%, 60%, 80%, 90%

Achieved sparsity is recorded separately from requested sparsity.

**Iterative Pruning and Fine-Tuning**

A supplementary CIFAR-10 experiment investigates iterative:

prune → fine-tune → re-prune

The experiment examines whether fine-tuning allows the surviving network to adapt following structural sparsification.

Cumulative sparsity levels of approximately:

0%, 20%, 36%, 48.8%, 59%, 67.2%

were investigated.

This experiment uses a single trained network per architecture and is therefore intended as an illustrative case study rather than a statistically generalised comparison.

**Graph Analysis**

Neural networks are represented as graphs in which neurons correspond to nodes and surviving neural connections correspond to edges.

The repository contains implementations for analysing structural properties including:

Graph connectivity
Largest connected component
Number of connected components
Spectral radius
Algebraic connectivity
Minimum node degree
Path-based structural measures

For the CIFAR-10 connectivity-preserving experiments, minimum degree is used as a primary structural bottleneck measure because the pruning procedure explicitly constrains per-neuron connectivity.

**Statistical Analysis**

The main CIFAR-10 magnitude-versus-random comparison uses five independently trained seeds per architecture.

Statistical comparisons are performed between the magnitude-pruned and random-pruned results for the evaluated predictive and structural metrics.

The iterative fine-tuning experiment is not included in the main statistical comparison because it uses a single seed per architecture.

**Requirements**

The experiments were implemented in Python using:

PyTorch
torchvision
NumPy
NetworkX
SciPy
Matplotlib
Seaborn


**Citation**

If you use this code or build upon the experimental methodology, please cite the associated dissertation:

Ashitha Ninganagouda Hiregoudra. Structural Analysis of Neural Network Pruning Using Graph Theory and Graphon Models. MSc Artificial Intelligence, University of Bath, 2026.
