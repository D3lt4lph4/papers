# OverFeat

_last modified : 19-07-2019_

## General Information

- Title: OverFeat: Integrated Recognition, Localization and Detection using Convolutional Networks
- Authors: Pierre Sermanet, David Eigen, Xiang Zhang, Michael Mathieu, Rob Fergus, Yann LeCun
- Link: [article](https://arxiv.org/abs/1312.6229)
- Date of first submission: 21 Dec 2013
- Implementations:
    - [C++](https://github.com/sermanet/OverFeat)

## Brief

This was one of the new generation of algorithm to greatly improve the results on the classification/localization/detection competition. The results are far from what's done today, but at the time it was a new approach of the problem using CNN.

The paper is divided in three main parts: Classification, Localization and Detection. They used a similar architecture that the one presented in the ImageNet classification paper from Krizhevsky et al.

Even if there are three networks presented in the article, one for classification, one for localization and one for detection, all of them are build on the same base.

Finally, to give an idea of the quality of the results, it was number one at the time on detection with a 24,3% mAP on the detection.

## How Does It Work

### Classification

This is the simplest task to carry: given an image, find the dominant object in it. They used an architecture similar to the ImageNet paper with a few improvements.

The most noticeable change is the use of the multi-scale image coupled with a sliding window. The interesting part is they apply the sliding window not at the start of the network, but in the middle of it just before the dense layers. This way they avoid recomputing the whole feature extraction.

At test time they also replace the dense layer with convolutional ones making the whole network a series a convolutions/pooling.

### Localization

Basically this is the same process as the classification task, the classification layers being replaced with a regression layer to get the boxes. The sliding windows are applied the same way as before.

The final step is to merge the bounding boxes for each window/scale to guess the position of the object in the image.

### Detection

To clarify things, the difference between Localization and Detection is the presence of a background label for the detection when no object is present. It is also to be noted that for the detection task, in many images, the objects can be much smaller.

The network used is the same as for the Localization, the difference is in the training. Negative training is performed with bootstrapping.


## Results

For Localization and detection it is not specified if the results are for the fast or big architecture.

|Network|Classification (error rate)|Localization (error)|Detection (mAP)|
|-|:-------------------------:|:------------------:|:-------------:|
|Fast|13,6%|-|-|
|Big |14,2%|-|-|
|Undefined|-|29,9%|24.3%|
