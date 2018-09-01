#  Photographic Image Synthesis with Cascaded Refinement Networks

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



## In Depth

