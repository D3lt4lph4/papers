# Stochastic gradient descent

This section will describe in details the algorithm of the Stochastic gradient descent (SGD) as well as the intuition behind it. Support for testing the algorithm will soon be available.


The SGD is a modified version of the "standard" gradient descent method. The standard method consist in calculating the gradient using the following formula:

\[
w += - \eta \sum_{i=1}^{n} Q_i(w)
\]