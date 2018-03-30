# YOLO

## General Information

- Title: You Only Look Once: Unified, Real-Time Object Detection
- Authors: Joseph Redmon, Santosh Divvala, Ross Girshick, Ali Farhadi
- Link: [article](https://arxiv.org/abs/1506.02640)
- Date of first submission: 8 Jun 2015
- Implementations:
    - [Darknet](https://github.com/pjreddie/darknet)

## Brief

YOLO is a novel approach for the object detection in images. The main difference with the previous approaches is that it is a one shot detector, meaning you only do one pass to get all of your boxes with labels on the images. The counter part to that approach is the limited number of possible detections on one image (potentially up to 98 boxes on the PASCOL VOC version of the network) but in the trade, the number of fps max is greatly improved (up to 45 fps on a Titan X GPU) and the mAP is good at 63,4% on the PASCAL VOC 2007 dataset. It is also to be noted there is a smaller version of the network which goes up to 150 fps but at the cost of a loss in the mAP (52,7%).



## How Does It Work

The architecture of the network is quite simple even if some details are unclear when it comes to the size of the boxes.

The following diagram taken from the article shows the layers of the network:

[YOLO architecture](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/yolo/network.png "YOLO")

The network is a classical series of convolutional and pooling layers (pooling not shown on the diagram) followed by two fully connected layers.

The important part of the network is the last fully connected layer which contains all the information. Basically it is of size SxSx(B*5+C), so in the diagram 7x7x30. The S is the granularity of your output, B the number of bounding boxes and C the number of classes.

## Results

The final results take from the article are the following ones:

- VOC 2007

| Network | mAP | Combined | Gain |
|---------|:---:|:--------:|:----:|
| Fast R-CNN | 71.8 | - | - |
| Fast R-CNN (2007 data) | 66.9 | 72.4| .6 |
| Fast R-CNN (VGG-M) | 59.2 | 72.4 | .6 |
| Fast R-CNN (CaffeNet) | 57.1 | 72.1 | .3 |
| YOLO | 63.4 | 75.0 | 3.2 |

- VOC 2012

| Network | mAP |
|---------|:---:|
| Fast R-CNN + YOLO | 70,7 |
| Faster R-CN | 70,4 |
| YOLO | 57,9 |

Among the results, one interesting thing is the mixing of their method with others to improve the mAP the two had separately.

## In Depth

There is a great explanation of the more obscure point of the network [here](http://christopher5106.github.io/object/detectors/2017/08/10/bounding-box-object-detectors-understanding-yolo.html), I greatly recommend to go check it out for more detail on the network.