# R-FCN

## General Information

- Title: R-FCN: Object Detection via Region-based Fully Convolutional Networks
- Authors: Jifeng Dai, Yi Li, Kaiming He, Jian Sun
- Link: [article](https://arxiv.org/abs/1605.06409)
- Date of first submission: 20 May 2016
- Implementations: (if any found)
    - [Matlab](https://github.com/daijifeng001/R-FCN)
    - [Python/Caffe](https://github.com/YuwenXiong/py-R-FCN)

## Brief

This network is like a "fork" of the Faster R-CNN, the idea for the classification is the same, the part that changes is the classification at the end (full convolutional + pooling instead of the Fast R-CNN classifier). They also changed the first model used to extract the feature from the image, in the Faster R-CNN, the VGG-16 is the classifier used (other were tested), in this one, the ResNet-101 is used.
According to the paper, they can go 2.5 to 20 times faster than a Faster R-CNN with the ResNet-101 and get results of 83,6% of mAP on the PASCAL VOC 2007 and 82,0% on the 2012.

## How Does It Work

As said before, the architecture of the network is kind of the same as the architecture of the Faster R-CNN, the image below (taken from the article) shows the architecture of the network:

![Network architecture](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/rfcn/network.jpg "R-FCN")

The first part is the feature maps, these are extracted from the image using the ResNet-101. Then at this point the architecture diverge from the Faster R-CNN. There is still the RPN network, but also, the feature map is given to a set of convolutional layers to create a set of grid that will be used in combination with the ROI extracted from the feature maps to tell if the ROI correspond to an object, and if so, which one.

## In Depth

Now lets go a bit more in to the details of the last part of the network,the ROI + vote.

Also taken from the paper, this diagram describes in details the last part of the network:

![Network details](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/rfcn/networkdetails.png "R-FCN")

This is almost the same image as before, only with a bit more details on the shapes. From now on, "bins layers" will refer to the colored layer obtained from the feature maps after the convolutions.

The idea is the following, the ROI is cut down into N bins, here k*k, each of this bin correspond to one of the bins layers. For instance, the light blue bins layer correspond to the bottom-right bin of the ROI. This way, to each bin of the ROI a class is assigned (C+1 for the number of classes + background). Finally from those N bins, the final class is extracted with a confidence index.
