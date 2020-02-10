# ResNet

_last modified : 10-02-2020_

## General Information 

- Title: Deep Residual Learning for Image Recognition
- Authors: Kaiming He, Xiangyu Zhang, Shaoqing Ren and Jian Sun
- Link: [article](https://arxiv.org/abs/1512.03385)
- Date of first submission: 10 Dec 2015
- Implementations: Natively available in most if not all the frameworks

## Brief

In this paper, the authors present a new method to train very deep neural networks more easily. They evaluate on the ImageNet dataset and carry a more detailed study on a smaller dataset: MNIST.

The main contribution is the introduction of residual layers. The main idea is to give the network the possibility to bypass the convolution layers if required. Through these layers they are able to train network going up to 152 layers deep.

## How Does It Work

They start the reflection from a simple ascertainment, a deeper network should, in practice be able to obtain at least the accuracy of a shallower one. Indeed, if we were to make a network from a shallower one, by setting all the added layers so that they act as an identity function, the end result should be the same. Yet deeper network tend not to train as well as their shallow counterpart.

In order to improve the results, they introduce the residual connections (c.f image below).

![Connection](https://github.com/D3lt4lph4/papers/blob/master/docs/images/imageclassif/resnet/residual.png?raw=true "Connection")


By adding the identity arrow on the right, they give to the network the possibility to very easily act as an identity layer if it was to be required.


## Results

They won many competitions, starting with the ILSVRC 2015 classification task. They also won the 1st places on the tasks of ImageNet detection, ImageNet local-ization, COCO detection, and COCO segmentation.

The ILSVRC top-5 error is presented below. The other results are not, but to summarize them, the deeper the ResNet network, the better. They tested up to 152 layers in their network.

| method | top-5 err. (test) |
|:-:|:-:|
| VGG (ILSVRC’14) | 7.32 |
| GoogLeNet (ILSVRC’14) | 6.66 |
| VGG | 6.8 |
| PReLU-net | 4.94 |
| BN-inception | 4.82 |
| ResNet (ILSVRC’15) | 3.57 |
