# ImageNet Classification with Deep Convolutional Neural Networks

## General Information

- Title: ImageNet Classification with Deep Convolutional Neural Networks
- Authors: Alex Krizhevsky, Ilya Sutskever, Geoffrey E. Hinton
- Link: [article](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)
- Date of first submission: 2012
- Implementations:

## Brief

The network presented in this paper improved by a large margin the results on the challenges from back then. The network consists, as described in the paper, of five convolutional layers, some of which are followed by max-pooling layers, and three fully-connected layers with a final 1000-way softmax. 
In order to improve the results, they used novel techniques such as the ReLU activation function, local normalization and dropout layers.

## How Does It Work

The following figure describe the architecture of the network, it is divided into two parts (top/bottom) because the network was trained on two gpus and needed a specific architecture to fit into memory. It is to be noted that at the time, the memory available for the GPU was limiting the size of the network.

![Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/imagenet/imagenet_network.jpg "Network")

## Results

Comparison of results on ILSVRC-2010 test set (the lower the better, last line Krizhevsky network).

| Model | Top-1 | Top-5 |
|-------|-------|-------|
| Sparse coding | 47,1 % | 28,2 % |
| SIFT + FVs | 45,7 % | 25,7 % |
| CNN | 37,5 % | 17,0 % |

Comparison of error rates on ILSVRC-2012 validation and test sets. First line are best results achieved by others.  Models with an asterisk* were “pre-trained” to classify the entire ImageNet 2011 Fall release :

| Model | Top-1 (val) | Top-5 (val) | Top-5 (test) |
|-------|-------------|-------------|--------------|
| SIFT + FVs | -- | -- | 26,2 % |
| 1 CNN | 40,7 % | 18,2 % | -- |
| 5 CNNs | 38,1 % | 16,4 % | 16,4 % |
| 1 CNN* | 39,0 % | 16,6 % | -- |
| 7 CNNs* | 36,7 % | 15,4 % | 15,3 % |

## In Depth

This is a classical architecture for image classification with the use of convolution layers followed by pooling layers. 
There is one thing to be noticed in the article, it's the specialization of each of the gpu. It seems that each time they trained the network, one tend to be color-agnostic, while the other was color specific.

As specified in the paper, a network this size is very sensitive to overfitting, even given the size of the training set (1.2 million labelled training examples). That's why they used dropout layers and specific data-augmentation (image translation, flips and alteration in the RGB channels).
