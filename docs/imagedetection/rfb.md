# Receptive Field Block Net for Accurate and Fast Object Detection

_last modified : 09-11-2018_

## General Information

- Title: Receptive Field Block Net for Accurate and Fast Object Detection
- Authors: Songtao Liu, Di Huang, Yunhong Wang
- Link: [article](https://arxiv.org/abs/1711.07767)
- Date of first submission: Tue, 21 Nov 2017
- Implementations:
    - [PyTorch](https://github.com/ruinmessi/RFBNet)

## Brief

This article introduce a new module, the RF Block (RFB) inspired by the Receptive Fields (RFs) in the human visual systems. This is the main contribution of the article, the network they use is strongly based on the [SSD](https://arxiv.org/abs/1512.02325). The idea is to improve the precision of the one stage networks by copying the pattern of the neurones in the human visual cortex. They get results on par with the state of the art detector while keeping the speed advantage of the one stage classifiers.

## How Does It Work

The architecture of the network is shown in the following figure and is basically an SSD with some of the layers replaced by the RFB module. The backbone network is still a VGG16 and the prediction is still made by a cascade of convolutions.

![RFB Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/rfb/rbf_network.png "RFB Network")

Basically the idea is to look wider, as show in the following figure:

![RFB module activation](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/rfb/rbf_spatial_precision.png "RFB module activation")

More region are activated by the module.

## Results

Comparison of results for detection on the VOC 2007:

        | Model | mAP | fps |
        | Faster RCNN | 73.2 \% | 7 |
        | R-FCN | 80.5 \% | 9 |
        | YOLOv2 544 | 78.6 \% | 40 |
        | R-FCN w deformable CNN | 82.6 \% | 8 |
        | SSD300 | 77.2 \% | 46 |
        | RFB Net300 | 80.5 \% | 43 |
        | RFB Net512 | 82.2 \% | 18 |

Comparison of results for classification on COCO dataset:

       | Method | Backbone | Data | Time | Avg. Precision, IoU: 0.5:0.9 |
       | Faster | VGG | trainval |147 ms | 24.2 |
       | Faster+++ | ResNet-101 | trainval | 3.36 s | 34.9 |
       | Faster w FPN | ResNet-101-FPN | trainval35k | 240 ms | 36.2 |
       | Faster by G-RMI | Inception-Resnet-v2 | trainval | – | 34.7 |
       | R-FCN | ResNet-101| trainval | 110 ms | 29.9 |
       | R-FCN w Deformable CNN  | ResNet-101| trainval | 125 ms | 34.5 |
       | Mask R-CNN  | ResNext-101-FPN| trainval35k | 210 ms| 37.1 |
       | YOLOv2  | darknet| trainval35k | 25 ms | 21.6 |
       | SSD300*  | VGG| trainval35k | 22 ms | 25.1 |
       | SSD512*  | VGG| trainval35k | 53 ms | 28.8 |
       | DSSD513  | ResNet-101| trainval35k | 182 ms | 33.2 |
       | RetinaNet500  | ResNet-101-FPN| trainval35k | 90 ms | 34.4 |
       | RetinaNet800 | ResNet-101-FPN| trainval35k | 198 ms | 39.1 |
       | RFB Net300 | VGG | trainval35k | 25 ms | 29.9 |
       | RFB Net512 | VGG | trainval35k | 55 ms | 33.8 |
       | RFB Net512-E | VGG | trainval35k | 59 ms | 34.4 |

## In Depth

They introduce two different module, the rfb_a and rfb_b. In conception they are both very similar, the internal layer is the only part changing, cf figures.

![RFB module a](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/rfb/rbf_module_a.png "RFB module a")

![RFB module activation](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/rfb/rbf_module_b.png "RFB module b")

For each of the two modules, the principal change compared to an inception module is the presence of the dilated convolutions.