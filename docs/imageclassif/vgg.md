# VGG

_last modified : 16-07-2019_

## General Information (main fields described, non-exhaustive list)

- Title: Very Deep Convolutional Networks for Large-Scale Image Recognition
- Authors: Karen Simonyan, Andrew Zisserman
- Link: [article](https://arxiv.org/abs/1409.1556)
- Date of first submission: 4 September 2014
- Implementations: Built-in for most of the deep-learning framework 

## Brief

This article tests the importance of depth for neural networks. To do so, they train multiple neural networks, slowly increasing the depth of each of the networks. 

## How Does It Work

There are multiple networks trained in the article, all of the architecture are describe in the figure below. The networks are series of convolutions and pooling followed by fully connected layers.

![Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/vgg/vgg_architectures.png "Networks")
## Results

The table below describes all the results obtained on the ILSVRC challenge.

 

| Method | top-1 val. error (\%) | top-5 val. error (\%)| top-5 test error (\%) |
|--------|-----------------------|----------------------|-----------------------|
| VGG (2 nets, multi-crop \| dense eval.) | 23.7 | 6.8 |6.8 |
| GoogLeNet (Szegedy et al., 2014) (1 net) | - | 7.9 | 7.9 |
| GoogLeNet (Szegedy et al., 2014) (7 nets) | - | 6.7 | 6.7 |
| MSRA (He et al., 2014) (11 nets) | - | - | 8.1 |
| MSRA (He et al., 2014) (1 net) | 27.9 | 9.1 | 9.1 |
| Clarifai (Russakovsky et al., 2014) (multiple nets) | - | - | 11.7 |
| Clarifai (Russakovsky et al., 2014) (1 net) | - | - | 12.5 |


And the table bleow describe the results obtained for the different architectures described in the section "How Does It Works". This table shows that increasing the depth of the network increase the precision of the results.


ConvNet config. | smallest image side | smallest image side test | top-1 val. error (\%) | top-5 val. error (\%) |
|---------------|---------------------|--------------------------|-----------------------|-----------------------|
B | 256 | 224,256,288 | 28.2 | 9.6 |
C | 256 | 224,256,288 | 27.7 | 9.2 |
C | 384 | 352,384,416 | 27.8 | 9.2 |
C | [256; 512] | 256,384,512 | 26.3 | 8.2 |
D | 256 | 224,256,288 | 26.6 | 8.6 |
D | 384 | 352,384,416 | 26.5 | 8.6 |
D |[ 256; 512] | 256,384,512 | 24.8 | 7.5 |
E | 256 | 224,256,288 | 26.9 | 8.7 |
E | 384 | 352,384,416 | 26.7 | 8.6 |
E | [256; 512] | 256,384,512 |24.8 |7.5 |


## In Depth

Nothing special, go check the article for details on the data-augmentation used or the experiments they did.
