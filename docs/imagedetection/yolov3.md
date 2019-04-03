# YOLOv3

_last modified : 25-03-2019_

## General Information

- Title:YOLOv3: An Incremental Improvement
- Authors: Joseph Redmon, Ali Farhadi
- Link: [article](https://arxiv.org/pdf/1804.02767.pdf)
- Date of first submission: 8 April 2018
- Implementations:
    - [Darknet](https://pjreddie.com/darknet/yolo/)
    - [Keras](https://github.com/xiaochus/YOLOv3)
    - [PyTorch](https://github.com/ayooshkathuria/pytorch-yolo-v3)

## Brief

This is the last version of the YOLO network, the authors share the new architecture of the network as well as the technical details for the implementation and the training of the network. According to the article, the network gets very good results (close to (but under) the state of the art for improved detection speed).

## How Does It Work

The same as the previous YOLO networks, one shot detectors, predicts the bounding boxes. The main difference is the network being a bit bigger.

## Results

COCO dataset:

| Network | mAP-50 | time (FPS) |
|:-------:|:------:|:----------:|
| SSD321 | 45.4 | 61 |
| DSSD321 | 46.1 | 85 |
| R-FCN | 51.9 | 85 |
| SSD513 | 50.4 | 125 |
| DSSD513 | 53.3 | 156 |
| FPN FRCN | 59.1 | 172 |
| RetinaNet-50-500 |50.9 | 73 |
| RetinaNet-101-500 | 53.1 |90 |
| RetinaNet-101-800 | 57.5 | 198 |
| YOLOv3-320 | 51.5 | 22 |
| YOLOv3-416 | 55.3 | 29 |
| YOLOv3-608 | 57.9 | 51 |

## In Depth

A lot of improvement were made, including:

- objectness, they add an objectness score to the boxes prediction to take into account the fact that many prior box may overlap an object
- Not using a softmax classifier (using a softmax make the assumption of not overlapping classes), instead a logistic classifier
- Multi-scale prediction, the network predicts feature at 3 scales and uses a system similar to feature pyramid network
- New feature extractor
