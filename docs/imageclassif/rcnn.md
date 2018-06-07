# RCNN

## General Information

- Title: Rich feature hierarchies for accurate object detection and semantic segmentation
- Authors: Ross Girshick, Jeff Donahue, Trevor Darrell, Jitendra Malik
- Link: [article](https://arxiv.org/pdf/1311.2524.pdf)
- Date of first submission: 11 November 2013
- Implementations:
    - [Caffe](https://github.com/rbgirshick/rcnn)

## Brief

This network is one of the pioneers for object detection. In its conception it is tightly linked to the OverFeat network, as described in the article : "OverFeat can be seen (roughly) as a special case of R-CNN.".

Even if the architecture of the network is inspired by OverFeat, the RCNN outperformed all of the results at the time og its publication. 

One of the main contribution of the paper is to demonstrate the gain obtained when pre-training on large auxiliary dataset and after that training on the target set (usally smaller).

This is not an end-to-end classifier as we can see nowadays.

## How Does It Work

The network is made of three main parts, the region extractor, the feature extractor and finally the classifier. The whole network is shown in the following image:

![RCNN Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/rcnn/rcnn_network.png "RCNN Network")

A region proposal algorithm extract ROI, then each region is fed to a classifier and finally the extracted features are classified.

## Results

The results are for two different data-set.

Results for the PASCAL VOC 2010 challenge :

| Model | mAP |
|-------|-----|
| RCNN | 53.7 |
| SegDPM | 40.4 |
| Regionlets | 39.7 |
| UVA | 35.1 |
| DPM | 33.4 |

Results for the ILSVRC 2013 challenge :

| Model | mAP |
|-------|-----|
| RCNN | 31.4 |
| OverFeat | 24.3 |

## In Depth

The first part of the network uses the selective search to generate around 2k boxes of possible objects. Then, second part of the network uses the network of the Krizhevsky et al to generate a  4096-dimensional feature vector from each boxes that were proposed. Finally the correct class is extracted using a SVM and Non-Maximum suppression from all the boxes.

## Warning

None so far.