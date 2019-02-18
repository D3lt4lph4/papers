# Dynamic Routing between Capsules

_last modified : 28-11-2018_

## General Information

- Title: Dynamic Routing between Capsules
- Authors: Sara Sabour, Nicholas Frosst, Geoffrey E. Hinton
- Link: [article](https://arxiv.org/abs/1710.09829)
- Date of first submission: 26 October 2017
- Implementations:
    - [All](https://github.com/topics/dynamic-routing-between-capsules)

## Brief

This paper introduce the notion of dynamic routing between capsules. A capsule is like a node of a tree in charge of the detection of a feature of an image. A capsule of an upper level will use the capsules of the lower level to predict the presence of an object. For instance if two lower level capsules get respectively head and body, with correct pose (i.e head up the body), then the next one should predict human.

## How Does It Work

The main contribution of the article is the routing. During the training process, the idea is that if the product scalar between the output of two capsule is high, then they agree and should "work" together. Using that, the connection between the capsules can be weighted during the training to give the correct results.

The following image shows the network used in the paper:

![Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/capsule/capsnet.png "Network")

Here two capsule layers are used, PrimaryCaps and DigitCaps. The computation of the DigitCaps layer works in the same way as any neural network (multiplication with the weights and sum), to the exception that the results of the multiplications are weighted to take into account the agreement with the previous capsule.

## Results

The MultiMNIST is the MNIST images fused together to have two digits on one image. The results are the error rate (the lower the better).

| Method | Routing | Reconstruction | MNIST (%) | MultiMNIST (%) |
|:-:|:-:|:-:|:-:|:-:|
| Baseline | - | - | 0.39 | 8.1 |
| CapsNet | 1 | no | 0.34+-0.032 | - |
| CapsNet | 1 | yes | 0.29+-0.011 | 7.5 |
| CapsNet | 3 | no | 0.35+-0.036 | - |
| CapsNet | 3 | yes | 0.25+-0.005 | 5.2 |

## In Depth

One of the very interesting part of their results is that they trained in parallel a network to reconstruct the images. And using the output vector of the classification (DigitCaps output) they can toy with some properties of the image, meaning they actually achieve the learning of some very specified features.
See image below:

![Image Modification](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/capsule/image_modification.png "Image Modification")

Since the whole idea of the capsule network is a bit complicated to explain in details here, please look at the two following links, [link_1](https://medium.com/ai%C2%B3-theory-practice-business/understanding-hintons-capsule-networks-part-i-intuition-b4b559d1159b), [link_2](https://hackernoon.com/what-is-a-capsnet-or-capsule-network-2bfbe48769cc), for more details on the subject (or read the paper ofc).