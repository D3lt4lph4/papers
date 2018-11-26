# FSSD

_last modified : 06-11-2018_

## General Information

- Title: FSSD: Feature Fusion Single Shot Multibox Detector
- Authors: Zuo-Xin Li, Fu-Qiang Zhou
- Link: [article](https://arxiv.org/pdf/1712.00960.pdf)
- Date of first submission: 4 December 2017
- Implementations:
    - [Pytorch](https://github.com/lzx1413/PytorchSSD)
    - [Caffe](https://github.com/lzx1413/CAFFE_SSD/tree/fssd)

## Brief

The FSSD is an improved version of the SSD. The authors try to add semantic information to improve the mAP, while at the same time not loose too much time in computation. 

## How Does It Work

The FSSD is very close to the SSD, the principle is exactly the same, a cascade of convolutional layers used to predict a set of boxes. The  difference is that the networks makes two passes on some layers to add information on the smaller boxes predicted (see image below):

![SSD/FSSD comparison](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/fssd/fssd.png "SSD/FSSD comparison")

## Results

The results shown here are the main results for the networks, some were omitted, look into the paper for more details.

Comparison of results for classification on the VOC 2007 test set :

| Model | train set | mAP | fps | gpu | backbone network |
|:-----:|:---------:|:---:|:---:|:---:|:----------------:|
| Faster RCNN | 07+12 | 73.2 | 7 | Titan X | VGGNet |
| Faster RCNN | 07+12 | 76.2 | 2.4 | K40 | ResNet-101 |
| SSD | 07+12+COCO | 81.2 | 46 | Titan X | VGGNet |
| SSD | 07+12 | 77.2 | 85 | 1080Ti | VGGNet |
| FSSD300 | 07+12+COCO | 82.7 | 65.8 | 1080Ti | VGGNet |

Comparison of results for classification on the VOC 2007 test set.

## In Depth

As said before, the main particularity of the network is two reuse computed feature maps to improve the accuracy of the network with out impeding too much the computation speed.

If one takes a look at the diagram in the first section, we can see that three layers are re-used before the the classification part. The selection is limited to those three layers because they think that the smaller layer at the end have too little information to be worth merging.

The merging is done using concatenation of the three layers and by resizing the smallest layers to the correct size using bilinear interpolation. To downsize the number of filers, they use 1x1 convolutions.
