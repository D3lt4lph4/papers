#  Photographic Image Synthesis with Cascaded Refinement Networks

_last modified : 02-09-2018_

## General Information

- Title: Photographic Image Synthesis with Cascaded Refinement Network
- Authors: Qifeng Chen, Vladlen Koltun
- Link: [article](https://arxiv.org/abs/1707.09405)
- Date of first submission: 28 July 2017
- Implementations:
    - [Tensorflow](https://github.com/CQFIO/PhotographicImageSynthesis)

## Brief

This paper present a method to generate realistic images from segmentation. 
Their method differs in the fact that they do not use adversarial training to learn the function to create the images.
They generate good quality images at high resolution (1024*2048) and they have a model that can generate images in different styles.

![Example of gen images](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagegeneration/photographicimagesynthesis/example.png "Example of gen images")

## How Does It Work

They make use of refinement modules to generate the image, and each module works with a power of two, that is, they start at 4x8, then 8x16, 16x32, ... , 1024x2048.
A refinement module is a series of convolution layers that takes as input a concatenation of the segmented image and the output of the previous refinement module.

And to create the set of tones for the images they go from output of (1024x2048x3) to (1024x2048x3*nb_tone). The training being done with a modified loss to avoid getting the same images. 

## Results

The results were tested using the Amazon Mechanical Turk platform and are summarized in the following graph (from the article):

![Results](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagegeneration/photographicimagesynthesis/graph_results.png "Results")

The test were the following, two image from two datasets were shown for a certain amount of time, and the annotator had to choose the most realistic one.

## In Depth

### Refinement Module

Each Refinement module is made up of 3 layers. 

First the input layer of dimension $w_i x h_i x (d_{i-1} + c)$ which is a concatenation of the previous refinement module and the semantic layout (respectively up and down sampled).
Then the intermediate and output layers of dimension $w_i x h_i x d_{i-1}$.

The layers are followed by convolutions, normalization and non-linearity functions depending on their position (c.f paper).

### Loss function

The loss function is adapted to let the network generate different images for the same input of segmented image.

The first idea of the loss is to use a network for classification, and to compare the inside layers rather than the output directly (to avoid, for instance, to force the color of object).
This gives the following : $\mathcal{L}_{I,L}(\theta) \sum_t \lambda_t \| \phi_l(I) - \phi_l(g(L,\theta))|_1$

Then, since the network generate m output image, they take the minimum of the previous function to force the outputs to cover the range of possible outputs.

Finally they do the same, semantic object per semantic object to cover the whole spectrum of possible representation for the objects.
