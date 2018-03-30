# OverFeat

## General Information (main fields described, non-exhaustive list)

- Title: OverFeat: Integrated Recognition, Localization and Detection using Convolutional Networks
- Authors: Pierre Sermanet, David Eigen, Xiang Zhang, Michael Mathieu, Rob Fergus, Yann LeCun
- Link: [article](https://arxiv.org/abs/1312.6229)
- Date of first submission: 21 Dec 2013
- Implementations:
    - [C++](https://github.com/sermanet/OverFeat)

## Brief

To give a bit of context, this is an old article regarding the field of machine learning. Basically this was one of the new generation of algorithm to greatly improve the results on the classification/localization/detection competition. The results are far from what's done today, but at the time it was a new approach of the problem using CNN.

The paper is divided in three main parts: Classification, Localization and Detection. They used a similar architecture to the one presented in the ImageNet. 

Even if the article presents three separate parts, all of them are build on the same model.

Finally, to give an idea of the results, it was number one at the time on detection with a (now low) 24,3% mAP on the detection.

## How Does It Work

Each of the network for the three challenges will be detailed thereafter, but first let's notice that they were using multiple classifiers to get their results (a bit in the idea of random forest). Also, they have two versions of their networks, one fast and one accurate.

### Classification

This is the simplest task to carry, given an image, find the dominant object in it. They used an architecture similar to the ImageNet paper with a few improvements.

The most noticeable change is the use of the multi-scale image coupled with a sliding window. The interesting part is they apply the sliding window not at the start of the network, but in the middle of it just before the dense layers. This way they avoid recomputing the whole feature extraction and make use of the properties of the convolutional layers.
At test time they also replace the dense layer with convolutional ones making the whole network a series a convolutions/pooling.

Then it is just a mixing of the results to get the correct classification

### Localization

Basically this is the same process as the classification task, the classification layers being replaced with a regression layer to get the boxes. The sliding windows are applied the same way as before.

The final step is to merge the bounding boxes for each window/scale to guess the position of the object in the image.

### Detection

To clarify things, the difference between Localization and Detection is the presence of a background label for the detection when no object is present. It is also to be noted that for the detection task, in many images, the objects can be much smaller.

Basically the same pattern as Localization, small difference in the training to get the background class.

## Results

For Localization and detection it is not specified if the results are for the fast or big architecture.

||Classification (error rate)|Localization (error)|Detection (mAP)|
||:-------------------------:|:------------------:|:-------------:|
|Fast|13,6%|-|-|
|Big |14,2%|-|-|
|Undefined|-|29,9%|24.3%|

## In Depth

To come