# CoordConv

## General Information

- Title: An intriguing failing of convolutional neural networks and the CoordConv solution
- Authors: Rosanne Liu, Joel Lehman, Piero Molino, Felipe Petroski Such, Eric Frank, Alex Sergeev, Jason Yosinski
- Link: [article](https://arxiv.org/abs/1807.03247)
- Date of first submission: 9 Jul 2018
- Implementations:
    - Tensorflow: Check the paper, implementation in the appendices

## Brief

This article present a new layer for convolutional neural networks.
The problems they are trying to solve are the two following ones (they apply later in the article the layer on other types of problems):

- Given two coordinates, generate a black dot on a grid at the indicated position
- Given a grid with a black dot, git the position of the dot.

They found that, for this kind of tasks, convolutions perform poorly.

## How Does It Work

The idea of the layer is very simple, two layers, one with the x coordinates and one with the y coordinates (see figure below).

![Layer](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/others/coordconv/uber_coordconv_layer.png "Layer")

The only concern one may have with this layer is to see the convolution losing its translations invariance properties. But since the layer will choose if it uses the CoordConv filters (setting weights to zero or not), it's actually not losing any properties.

## Results

This figure from the paper show some exemples of the improvement for the toy problem :

![Results](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/others/coordconv/uber_coordconv_results.png "Results")

## In Depth

For more details, check the Uber blog [here](https://eng.uber.com/coordconv/)
