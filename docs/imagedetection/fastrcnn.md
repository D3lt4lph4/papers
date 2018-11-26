# Fast R-CNN 

_last modified : 06-11-2018_

## General Information

- Title: Fast R-CNN 
- Authors: Ross Girshick
- Link: [article](https://arxiv.org/pdf/1504.08083.pdf)
- Date of first submission:  30 April 2015
- Implementations:
    - [Caffe](https://github.com/rbgirshick/fast-rcnn)

## Brief

This network is an improved version of the R-CNN network from the same author. The article claim the Fast R-CNN to train 9 times faster than the R-CNN and to be 213 times faster at test time. It also has a better mAP than the R-CNN, 66% vs 62%.

The main improvement of the network is to share the computation of the feature to avoid recomputing them for each box proposed by the region proposal algorithm (see below).

## How Does It Work

The network is a 3 modules network. The first one is the region proposal, the second one is the feature extractor network and finally the last one is the classifier/regressor. 

The region proposal, selects a set of potential boxes, then using the features extracted by the CNN network the classifier/regressor outputs the class of each boxes. 

The whole architecture is describe in the image thereafter:

![Fast RCNN Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/fastrcnn/fast_rcnn_network.jpeg "Fast RCNN Network")

## Results

The results are in that order, PASCAL VOC 2007, 2010 and 2012.

Comparison of results for classification on the VOC 2007:

| Model | train set | mAP |
|-------|-----------|-----|
| RCNN | 07 | 66.0 |
| Fast RCNN | 07 | 66.9 |
| Fast RCNN | 07 without difficult | 68.1 |
| Fast RCNN | 07+12 | 70.0 |

Comparison of results for classification on the VOC 20010:

| Model | train set | mAP |
|-------|-----------|-----|
| RCNN | 12 | 62.9 |
| Fast RCNN | 12 | 66.1 |
| Fast RCNN | 07+12 | 68.8 |

Comparison of results for classification on the VOC 2012.

| Model | train set | mAP |
|-------|-----------|-----|
| RCNN | 12 | 62.4 |
| Fast RCNN | 12 | 65.7 |
| Fast RCNN | 07+12 | 68.4 |

## In Depth

The workflow of the network is the following one:

- First RoIs are extracted from the image using the region proposal module;
- Then the input image is fed to the feature extractor module to output a feature map;
- Using the RoI pooling layer, a fixed length vector is extracted from the feature map for each proposal;
- Finally, these fixed length vectors go through fully connected layer to give two different outputs, one with the classes and the other one with the coordinates corrected of the bounding box (nms after to remove duplicate predictions).

### The RoI pooling layer

In order to extract fixed size map, let's say (7x7) the same as in the paper, the RoI pooling layer adapts the size of the max pooling used to the size of the proposed region.
The proposed RoI is divided into a grid of sub-area giving the desired output size. For instance a RoI of size (21x14) would be divided in blocks of size (3x2), each of these blocks is then max-pooled to give the (7x7) map.

### Mini-batch for fast training

To accelerate the training, when processing a batch of size M, rather than using M images with one RoI in each image, they use N image with M/N RoI. For instance, "when using N = 2 and M = 128, the proposed training scheme is roughly 64 times faster than sampling one RoI from 128 different images". The main advantage of this technique is to share the computation of the feature map for M/N data. They claim this technique not to impede the training of the network.
