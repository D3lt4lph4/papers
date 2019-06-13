# YOLO9000

_last modified : 13-06-2019_

## General Information

- Title: YOLO9000: Better, Faster, Stronger
- Authors: Joseph Redmon, Ali Farhadi
- Link: [article](https://arxiv.org/abs/1612.08242)
- Date of first submission:25 December 2016
- Implementations:
    - [darknet](https://github.com/pjreddie/darknet)
    - [Tensorflow](https://github.com/WojciechMormul/yolo2)

## Brief

This is an improved version of the YOLO network. It was designed to palliate to some defect of the YOLO: the precision of the network and the level of recall. On top of that, the new version can now predict up to 9000 classes and predict unseen classes.

## How Does It Work

The main idea stays the same as for the YOLO network, but the last layers are not fully connected but convolutional ones. The number of convolutional layers is increased, but since the fully connected layers are removed, the speed is not impacted.

## Results

Only the main results are show here, for more go check the article.

PASCAL VOC 2007 detection results:

| Network | Train | mAP | FPS |
|:-------:|:-----:|:---:|:---:|
| Fast R-CNN | 2007+2012 | 70.0 | 0.5 |
| Faster R-CNN VGG-16 | 2007+2012 | 73.2 | 7 |
| Faster R-CNN ResNet | 2007+2012 | 76.4 | 5 |
| YOLO | 2007+2012 | 63.4 | 45 |
| SSD300 | 2007+2012 | 74.3 | 46 |
| SSD500 | 2007+2012 | 76.8 | 19 |
| YOLOv2 288x88 |2007+2012  | 69.0 | 91 |
| YOLOv2 352x352 | 2007+2012  | 73.7 | 81 |
| YOLOv2 416x416 | 2007+2012  | 76.8 | 67 |
| YOLOv2 480x480 | 2007+2012  | 77.8 | 59 |
| YOLOv2 544x544 | 2007+2012|78.6 | 40 |
 
PASCAL VOC2012 test detection results:

| Network | data | mAP |
|:-------:|:----:|:---:|
| Fast R-CNN |07++12 |68.4|
| Faster R-CNN |07++12 |70.4|
| YOLO |07++12 |57.9 |
| SSD300 |07++12 |72.4|
| SSD512 |07++12 |74.9 |
| ResNet |07++12 |73.8 |
| YOLOv2 544 | 07++12 |73.4|

## In Depth

The new version of the YOLO uses many techniques to improve the results of the previous version.

The first two methods used are batch normalization and increase in the resolution of the input images. They add batch normalization on every convolutional layer of the network to get an improvement of mAP of 2%. And they increase the size of resolution for detection to 448x448 and get a 4% increase in the mAP.

The other improvements is the use of anchor boxes picked using the k-means algorithm. They use the k-means algorithm to pick anchor boxes fitting best the distribution of their objects to detect in the images.

Finally they changed the dimension of the input images during the training to have their network learn to do multi scale classification.
