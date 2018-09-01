# R-CNN

_last modified : 01-09-2018_

## General Information

- Title: Rich feature hierarchies for accurate object detection and semantic segmentation
- Authors: Ross Girshick Jeff Donahue Trevor Darrell Jitendra Malik
- Link: [article](https://arxiv.org/abs/1311.2524)
- Date of first submission: 11 Nov 2013
- Implementations:
    - [Original/Caffe](https://github.com/rbgirshick/rcnn)

## Brief

This is on if the first method to use CNN to do the detection task. At the time of the publication of the paper, it was making a break through regarding the results yield (new method have taken the lead since). The really novel part was to combine region proposal with CNN to classify the results.

## How Does It Work

A bit like above but more in details.

# Results

The results are the ones given on the github containing the original implementation.

Method         | VOC 2007 mAP | VOC 2010 mAP | VOC 2012 mAP
-------------- |:------------:|:------------:|:------------:
R-CNN          | 54.2%        | 50.2%        | 49.6%
R-CNN bbox reg | 58.5%        | 53.7%        | 53.3%

## In Depth

Here, go full description, tricks and all, keep in mind this is to explain the paper, but still a summary.