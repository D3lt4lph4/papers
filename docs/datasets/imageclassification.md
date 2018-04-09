# Datasets for image classification

Here are listed all the datasets that can be used for image classification. Each dataset should come with a small description of its size, what's in it and who provided it.

## The UA-DETRAC Benchmark Suite

This dataset is both for multi-object detection and multi-object tracking.

- Contains:
    - Vehicles: Cars, Bus, Van, Other
    - Weather: cloudy, sunny, rainy, night
    - Different level of occlusion

- Size:
    - more than 140 thousand frames
    - 8250 vehicles manually annotated
    - 1.21 million labeled bounding boxes of objects

- Other details:
    - location: 24 different locations at Beijing and Tianjin in China
    - 10 hours of videos captured with a Cannon EOS 550D camera

- Article:
    - Authors: Longyin Wen, Dawei Du, Zhaowei Cai, Zhen Lei, Ming{-}Ching Chang, Honggang Qi, Jongwoo Lim, Ming{-}Hsuan Yang and Siwei Lyu
    - Link: [article](https://arxiv.org/abs/1511.04136)

- Book:
    - Title: UA-DETRAC 2017: Report of AVSS2017 \& IWT4S Challenge on Advanced Traffic Monitoring
    - Authors: Lyu, Siwei and Chang, Ming-Ching and Du, Dawei and Wen, Longyin and Qi, Honggang and Li, Yuezun and Wei, Yi and Ke, Lipeng and Hu, Tao and Del Coco, Marco and others
    - pages: 1--7

- Dataset: [here](http://detrac-db.rit.albany.edu/)

## The KITTI Vision Benchmark Suite

This dataset is both for multi-object detection and multi-object tracking.

- Contains:
    - Tracking: 8 classes but only 'Car' and 'Pedestrian' have enough instance according to the website
    - Detection / 2D Objects: Unspecified on website, cars at least
    - Detection / 3D Objects: Unspecified on website, cars at least
    - Detection / bird's eye view: Cars (maybe)

- Size:
    - Tracking: 21 training sequences and 29 test sequences
    - Detection / 2D Objects: 7481 training images and 7518 test images
    - Detection / 3D Objects: 7481 training images and 7518 test images
    - Detection / bird's eye view: 7481 training images and 7518 test images for 80 256 labeled objects
- Dataset: [here](http://www.cvlibs.net/datasets/kitti/index.php)