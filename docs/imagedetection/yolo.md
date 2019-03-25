# YOLO

_last modified : 25-03-2019_

## General Information

- Title: You Only Look Once: Unified, Real-Time Object Detection
- Authors: Joseph Redmon, Santosh Divvala, Ross Girshick, Ali Farhadi
- Link: [article](https://arxiv.org/abs/1506.02640)
- Date of first submission: 8 Jun 2015
- Implementations:
    - [Darknet](https://github.com/pjreddie/darknet)

## Brief

YOLO is a one shot detectors, meaning that it only does one pass on the images to output all the detections. The obvious advantage in this method is the speed up in the computation and the increase in the number of frame being processed by second. The downside of this method is to have mAP a bit under the top classifiers.

## How Does It Work

The architecture of the network is quite simple, it is a series of convolutional layers followed by fully connected layers.

The following diagram shows the layers of the network:

![YOLO architecture](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/yolo/network.png "YOLO")

The main idea is to have a grid of boxes to cover all the image being processed. The last layer contains all the boxes, coordinates and classes. This way you can cover the whole image with a pre-defined set of boxes.

## Results

The final results take from the article are the following ones:

- VOC 2012

| Network | mAP |
|---------|:---:|
| Fast R-CNN + YOLO | 70,7 |
| Faster R-CN | 70,4 |
| YOLO | 57,9 |

- Speed

| Real-Time Detectors | Train | mAP | FPS |
|---------------------|:-----:|:---:|:---:|
| 100Hz DPM | 2007 | 16.0 | 100 |
| 30Hz DPM | 2007 | 26.1 | 30 |
| Fast YOLO | 2007+2012 | 52.7 | 155 |
| YOLO | 2007+2012 | 63.4 | 45|

| Less Than Real-Time | Train | mAP | FPS |
|---------------------|:-----:|:---:|:---:|
| Fastest DPM | 2007 | 30.4 | 15 |
| R-CNN Minus R | 2007 | 53.5 | 6 |
| Fast R-CNN | 2007+2012 | 70.0 | 0.5 |
| Faster R-CNN VGG-16 | 2007+2012 | 73.2 | 7 |
| Faster R-CNN ZF | 2007+2012 | 62.1 | 18 |
| YOLO VGG-16 | 2007+2012 | 66.4 | 21 |

## In Depth

We will only detail quickly the way of work of the grid of boxes. For more details, check this [link](http://christopher5106.github.io/object/detectors/2017/08/10/bounding-box-object-detectors-understanding-yolo.html), it explains very clearly all the details of the network.

If we take a look at the image above (how does it works), we can see the size of the last layer to be 7x7x30, this is the output size for the PASCAL VOC challenge.

The 7X7 is the size of the grid (see image below), the 30 is for the 20 classes of the network + 2 boxes (4 coordinates and confidence). It is important to see that only one class probability is used for two boxes.

![yolo grid](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/yolo/yologrid.png "YOLO grid boxes")

Then, for each two boxes of the grid, the coordinates are regressed, meaning that a box can actually be way bigger than the size of the cell. After that, the usual processing of the boxes to get the output.
