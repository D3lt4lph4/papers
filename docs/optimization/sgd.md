# Stochastic gradient descent

## Original Version

This section will describe in details the algorithm of the Stochastic gradient descent (SGD) as well as the intuition behind it. Support for testing the algorithm will soon be available.


The SGD is a modified version of the "standard" gradient descent method. The standard method consist in calculating the gradient using the following formula:

\[
w = w - \eta \sum_{i=1}^{n} \nabla Q_i(w)
\]

One of the problems with this method is that it might be computionnaly costly as we have to calculate the gradient for each input.

The SGD (in its basic form) approximate the gradient by calculating it only for one of the input.

Basically we remove the summation term in the previous formula:

\[
w = w - \eta \nabla Q_i(w)
\]

Finally, the mini-batch version is an in between the two previous versions, rather than take only one or all, take a few.


## Variants

### SGD with Momentum

The idea behind this version of the SGD is to mimicate the way a ball could roll down a hill to its lowest point. Basically it adds some speed to the ball. The new formula is the following one:

\[
\nabla w = \alpha \nabla w - \eta \nabla Q(w)
w = w + \nabla w
\]

### Averaging SGD

Another version where the average is used instead of only the update.
THe formula used is the following one:

\[
\bar{w} = \frac{1}{N} \sum_{i=1}^{N} w_i
\]
