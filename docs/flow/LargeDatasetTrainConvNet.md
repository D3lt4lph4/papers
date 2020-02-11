# A Large Dataset to Train Convolutional Networks for Disparity, Optical Flow, and Scene Flow Estimation

_last modified : 11-02-2020_

## General Information

- Title: A Large Dataset to Train Convolutional Networksfor Disparity, Optical Flow, and Scene Flow Estimation
- Authors: Nikolaus Mayer, Eddy Ilg, Philip Häusser, Philipp Fischer, Daniel Cremers, Alexey Dosovitskiy, Thomas Brox
- Link: [article](https://arxiv.org/abs/1512.02134)
- Date of first submission: 7 Dec 2015
- Implementations:

## Brief

This paper aims to fully estimate optical flow, disparity and scene flow. The aim is to extend the work done on scene flow prediciton to the above cited tasks. In order to do so, they introduce three novel dataset as well a network DipsNet.

Using these datasets, they manage to train a neural network that correctly estimate the scene flow of images. They reach state of the art results on the disparity estimation and can predict the values faster.



## How Does It Work

### Introduced datasets

**FlyingThings3D**: This dataset is a bit like the chairs dataset except that it has objects flying in random 3D directions. They used random objects for the generation of the images. The object were add on a randomized background.

**Monkaa**: This dataset is extracted from the short film Monkaa. It was done using Blender and they added their own scenes to it.

**Driving**: This dataset was made to resemble the Kitti dataset. They again used blender to generate the images and downloaded models from an online database (3D Warehouse)

### Introduced network

For the estimation of the optical flows, they used a modified version of FlowNet. They proposed a basic architecture, DispNet for disparity estimation which is also based on FCN architecture. As in FlowNet, they introduced the network with the correlation between the first features but this time they used a 1D convolution instead of 2D. They find the 1D convolution to improve the results.

## Results

| Method | Driving | FlyingThings3D | Monkaa | Sintel Clean | Time |
|:-:|:-:|:-:|:-:|:-:|:-:|
| DispNet | 15.62 | 2.02 | 5.99 | 5.38 | 0.06s|
| DispNetCorr1D | 16.12 | 1.68 | 5.78 | 5.66 | 0.06s|
| DispNet-K | 19.67 | 7.14 | 14.09 | 21.29 | 0.06s|
| DispNetCorr1D-K | 20.40 | 7.46 | 14.93 | 21.88 | 0.06s|
| SGM | 40.19 | 8.70 | 20.16 | 19.62 | 1.1s|
| MC-CNN-fst | 19.58 | 4.09 | 6.71 | 11.94 | 0.8s|
| MC-CNN-acrt | - | - | - | - | 67s |