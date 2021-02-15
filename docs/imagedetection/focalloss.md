# Focal Loss for Dense Object Detection

## General Information

- Title: Focal Loss for Dense Object Detection
- Authors: Tsung-Yi Lin, Priya Goyal, Ross Girshick, Kaiming He, Piotr Dollar
- Link: [article](https://arxiv.org/abs/1708.02002)
- Date of first submission: 7 August, 2017
- Implementations:
    - [keras](https://github.com/fizyr/keras-retinanet)
    - [Caffe 2](https://github.com/facebookresearch/Detectron)

## Brief

This paper addresses the class imbalance problem faced by one-stage detector. To do so they present a novel loss for object detection, the focal loss. 

Historically there are two types of detector, the one-stage and the two-stage detectors. The one-stage detectors are the fastest while the two-stage are the more accurate. They link this difference in accuracy with the class imbalanced faced by the one-stage detectors. Indeed, during training, the one-stage models have to deal with numerous background examples, which impede the training.
 Usually to counter this negative effect, hard negative mining is used. Here they try the novel loss which reduce the impact of easily classified examples on the loss. Hence the network is not overwhelmed by background boxes and can learn to correctly detect the objects

They also propose a network architecture for object detection, RetinaNet.

## How Does It Work

The introduce loss is a modified form of the cross entropy loss. Instead of simply using the log they introduce a factor in the form $(1 - p_t)^\gamma. This way, the more accurate the prediction is, the less it will count in the loss. This allow to decrease the importance of easily classify examples and to only account for the difficult ones.

Focal loss: $FL(p_t) = - \alpha_t(1 - p_t)^\gamma log(p_t)$

They also use a prior distribution on the output layers to avoid instability in the training due to the overwhelming number of background boxes.

The architecture of the RetinaNet is shown below:

![pipeline](https://github.com/D3lt4lph4/papers/blob/master/docs/images/imagedetection/focalloss/network.png?raw=true "pipeline")

They use the ResNet as backbone, add pyramidal convolutions (FPN) and the box classification/regression layers.

## Results

The two tables show the results they obtain compared with other methods. The first table is two stage detectors and the second in one stage detectors.

| | backbone | AP | AP50 | AP75 | APS | APM | APL |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| *Two-stage detectors:* | | | | | | | |
| Faster R-CNN+++ | ResNet-101-C4 | 34.9 | 55.7 | 37.4 | 15.6 | 38.7 | 50.9 |
| Faster R-CNN w FPN | ResNet-101-FPN | 36.2 | 59.1 | 39.0 | 18.2 | 39.0 | 48.2 |
| Faster R-CNN by G-RMI | Inception-ResNet-v2 | 34.7 | 55.5 | 36.7 | 13.5 | 38.1 | 52.0 |
| Faster R-CNN w TDM | Inception-ResNet-v2-TDM | 36.8 | 57.7 | 39.2 | 16.2 | 39.8 | **52.1** |
| *One-stage detectors:* | | | | | | | |
| YOLOv2 | DarkNet-19 | 21.6 | 44.0 | 19.2 | 5.0 | 22.4 | 35.5 |
| SSD513 | ResNet-101-SSD | 31.2 | 50.4 | 33.3 | 10.2 | 34.5 | 49.8 |
| DSSD513 | ResNet-101-DSSD | 33.2 | 53.3 | 35.2 | 13.0 | 35.4 | 51.1 |
| **RetinaNet** | ResNet-101-FPN | 39.1 | 59.1 | 42.3 | 21.8 | 42.7 | 50.2 |
| **RetinaNet** | ResNeXt-101-FPN | **40.8** | **61.1** | **44.1** | **24.1** | **44.2** | 51.2 |