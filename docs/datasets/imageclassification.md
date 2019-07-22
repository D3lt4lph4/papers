# Datasets for image classification and detection

_last modified : 19-07-2019_

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
    - Title: UA-DETRAC: A New Benchmark and Protocol for Multi-Object Detection and Tracking
    - Authors: Longyin Wen, Dawei Du, Zhaowei Cai, Zhen Lei, Ming{-}Ching Chang, Honggang Qi, Jongwoo Lim, Ming{-}Hsuan Yang and Siwei Lyu
    - Link: [article](https://arxiv.org/abs/1511.04136)

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

- Article:
    - Title: Are we ready for Autonomous Driving? The KITTI Vision Benchmark Suite
    - Authors: Andreas Geiger and Philip Lenz and Raquel Urtasun
    - Link: [article](http://www.cvlibs.net/publications/Geiger2012CVPR.pdf)

- Dataset: [here](http://www.cvlibs.net/datasets/kitti/index.php)

## The Berkeley BBD100K

- Contains:
    - Vehicles: Bus, Light, Sign, Person, Bike, Truck, Motor, Car, Train, Rider
    - Weather: clear, partly cloudy, over-cast, rainy, snowy, foggy, dawn/dusk, daytime, night
    - Different level of occlusion
    - Segmentation
    - Different scenes, such as: residential, highway, city, street, ...
    - Lane marking

- Size:
    - 100,000 HD video sequences of over 1,100-hour driving experience;
    - 2D Bounding Boxes annotated on 100,000 images;
    - Segmentation over 10,000 diverse images with pixel-level and rich instance-level annotations;
    - Multiple types of lane marking annotations on 100,000 images.

- Other details:
    - location: Different location in the USA, New York, Berkeley, San Francisco

- Article:
    - Title: BDD100K: A Diverse Driving Video Database withScalable Annotation Tooling
    - Authors: Fisher Yu, Wenqi Xian, Yingying Chen, Fangchen Liu, Mike Liao, Vashisht Madhavan, Trevor Darrell
    - Link: [article](https://arxiv.org/pdf/1805.04687.pdf)

- Dataset: [here](http://bdd-data.berkeley.edu/)

## Cifar-10

- Contains:
    - airplane
    - automobile
    - bird
    - cat
    - deer
    - dog
    - frog
    - horse
    - ship
    - truck

- Size:
    - 60000 images divided into 6 batches with one for the tests
    - images of size 32x32

- Dataset: [here](https://www.cs.toronto.edu/~kriz/cifar.html)
