# CoordConv

_last modified : 12-07-2019_

## General Information

- Title: An intriguing failing of convolutional neural networks and the CoordConv solution
- Authors: Rosanne Liu, Joel Lehman, Piero Molino, Felipe Petroski Such, Eric Frank, Alex Sergeev, Jason Yosinski
- Link: [article](https://arxiv.org/abs/1807.03247)
- Date of first submission: 9 Jul 2018
- Implementations:
    - Tensorflow: Check the paper, implementation in the appendices

## Brief

The CCNs are now the norm when it comes to image processing. But curiously, this type of architectures fails on some simple examples. In this paper, they set-up different toy problems (for instance "given a white dot on a black background, output the position of the dot") and show that the convolution network fails remarkably. To solve this problem, they introduce a new type of layer, the CoordConv.

The main toy problems they are trying to resolve are the two following ones (they apply later in the article the layer on other types of problems):

- Given two coordinates, generate a black dot on a grid at the indicated position
- Given a grid with a black dot, git the position of the dot.

## How Does It Work

The idea of the layer is very simple, two feature maps, one with the x coordinates and one with the y coordinates (see figure below). This way, the convolution can "know" its position in the feature map.

![Layer](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/others/coordconv/uber_coordconv_layer.png "Layer")

The only concern one may have with this layer is to see the convolution losing its translation invariance property. But since the layer will choose if it uses the CoordConv feature maps (setting weights to zero or not), the convolution should still work fine with the translation properties.

## Results

This figure from the paper show some exemples of the improvements for the toy problems :

![Results](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/others/coordconv/uber_coordconv_results.png "Results")

## In Depth

For more details, check the blog [here](https://eng.uber.com/coordconv/)
