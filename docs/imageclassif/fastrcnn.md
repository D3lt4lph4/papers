# Fast R-CNN 

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

![Fast RCNN Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/fastrcnn/fast_rcnn_network.jpeg "Fast RCNN Network")

## Results

The results are in that order, PASCAL VOC 2007, 2010 and 2012:


| Model | train set | mAP |
|-------|-----------|-----|
| RCNN | 0.7 | 66.0 |
| Fast RCNN | 07 | 66.9 |
| Fast RCNN | 07 without difficult | 68.1 |
| Fast RCNN | 07+12 | 70.0 |

Comparison of results for classification on the VOC 2007.


| Model | train set | mAP |
|-------|-----------|-----|
| RCNN | 12 | 62.9 |
| Fast RCNN | 12 | 66.1 |
| Fast RCNN | 07+12 | 68.8 |

Comparison of results for classification on the VOC 2010.



| Model | train set | mAP |
|-------|-----------|-----|
| RCNN | 12 | 62.4 |
| Fast RCNN | 12 | 65.7 |
| Fast RCNN | 07+12 | 68.4 |

Comparison of results for classification on the VOC 2012.


The following table show the speed improvement of the network (S = small, M = medium, L = large):


| Model | test rate | test speed up |
|-------|-----------|-----|
| Fast RCNN S | 0.10 | 98x |
| Fast RCNN M | 0.15 | 80x |
| Fast RCNN L | 0.32 | 146x |
| RCNN S | 9.8 | 1x |
| RCNN M | 12.1 \% | 1x |
| RCNN L | 47.0 \% | 1x |

Comparison of time results for classification.


## In Depth

The workflow is the following, the whole image goes through the feature extractor, then the scaled box is extracted from the feature map, resized to a fix size output using a ROI pooling layer, finally, the pooled map goes through a network with two outputs to get both the class and the box for the proposed region.

The main advantage of this method over the R-CNN one is the calculation of the feature map only once. Also since, apart from the region proposal, the whole pipeline is a neural network, the back-propagation can be carried through the whole network at once, accelerating the training process.


## Warning

