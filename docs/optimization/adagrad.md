# Adagrad

- Title: Adaptive Subgradient Methods for Online Learning and Stochastic Optimization
- Authors: John Duchi, Elad Hazan, Yoram Singer
- Link: [article](http://www.jmlr.org/papers/volume12/duchi11a/duchi11a.pdf)
- Date of first submission: 2011

## Idea

The main idea behind this optimizer is to add weights to the update to make it a per-parameter learning rate. This algorithm was developped to imporve the gradient descent on data with sparse parameters.

The update formula is the following one:

\[
w = w - \eta diag(G)^{-frac{1}{2}} \circ g
\]

Where \[ \circ \] is the element wise product and:

\[
G = \sum^{t}_{\tau} g_{\tau} g_{\tau}^{\top}
\]

Where:

\[
g_{\tau} = \nabla Q_i (w)    
\]

As one can see, the more a feature j of g's appears in the vector and should be updated strongly, the greater the division of eta