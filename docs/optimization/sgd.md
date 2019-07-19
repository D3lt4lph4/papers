# Stochastic gradient descent

_last modified : 19-07-2019_

This section will describe in details the algorithm of the Stochastic gradient descent (SGD) as well as the intuition behind it. Different versions exists and a maximum of them will be reviewed.

## Original Version

The Stochastic Gradient Descent is an iterative method for optimizing an objective function (the function has to satisfy some properties such as being differentiable or subdifferentiable).

The SGD is a modified version of the "standard" gradient descent method. For instance, let's say we want to minimize the objective function described in the first formula below, with $w$ being the parameter to optimize. The standard method consist in calculating the gradient using the second formula. For each of the sample drawn $Q_i$, calculate the derivative $\nabla Q_i(w)$, average, multiply by the learning factor $\eta$ and update the parameter to try to find on of the minimums.

\[
Q(w) = \frac{1}{n} \sum_{i=1}^{n} Q_i(w)
\]

\[
w = w - \eta \sum_{i=1}^{n} \frac{\nabla Q_i(w)}{n}
\]

One of the problems with this method is that it might be computationally costly as we have to calculate the gradient (which can be expensive depending on the function)for each input.

To compensate for this, the SGD (in its basic form) approximate the gradient by calculating it only for one of the input.

Basically we remove the summation term in the previous formula to get the following one.
One of the problems with this method is that it might be computionnaly costly as we have to calculate the gradient for each input.

\[
w = w - \eta \nabla Q_i(w)
\]

Finally, the mini-batch version is an in between the two previous versions, rather than take only one or all, take a few.


## Variants

### SGD with Momentum

The idea behind this version of the SGD is to mimicate the way a ball could roll down a hill to its lowest point. Basically it adds some speed to the ball. The new formula is described below.
\[
w = w + \alpha \nabla w - \eta \nabla Q(w)
\]

### Averaging SGD

Another version where the average is used instead of only the update.
The formula used is the following one:

\[
\bar{w} = \frac{1}{N} \sum_{i=1}^{N} w_i
\]
