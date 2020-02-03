# SqueezeSegV2: Improved Model Structure and Unsupervised DomainAdaptation for Road-Object Segmentation from a LiDAR Point Cloud

_last modified : 03-02-2020_

## General Information

- Title: SqueezeSegV2: Improved Model Structure and Unsupervised DomainAdaptation for Road-Object Segmentation from a LiDAR Point Cloud
- Authors: Bichen Wu, Xuanyu Zhou, Sicheng Zhao, Xiangyu Yue and Kurt Keutzer
- Link: [article](https://arxiv.org/abs/1809.08495)
- Date of first submission: 22 Sep 2018
- Implementations: 
    - [tensorflow (SqueezeSeg)](https://github.com/BichenWuUCB/SqueezeSeg)

## Brief

This is the article following [SqueezeSeg](https://arxiv.org/abs/1710.07368). They bring multiple improvements, both regarding the network architecture and training and the usage of generated data.

They add four modules (Batch Normalization, LiDAR mask, focal loss, CAM module) to the network architecture to get about 7 points improvement on average on segmentation of the objects. And they also add four modules (Learned Intensity Rendering, Geodesic Correlation Alignment, Progressive Domain Calibration, CAM module) to correct as much as possible the domain gap between the generated data (GTAV) and the target domain (Kitti). With this,  they improve the detection on the Kitti dataset with a network trained on generated data by about 27 points.

## How Does It Work

### Improvement of the network

**BatchNormalization**: Check the first 20 minutes here for a quick recap on BatchNorm and the advantages.

**LiDAR mask**: They add a binary mask to given the network information about the missing pixels.

**Focal Loss**: See the here for more details. This loss helps to train on unbalanced datasets.

**Context Aggregation Module (CAM)**: Module introduced to help with the missing points in the training data and help mitigate the induced dropout effect.

See below for the updated architecture of the network.

![Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageseg/squeezeseg/network.png "Network")

### Training on generated data

**Intensity rendering**: To solve the problem of missing intensity values in the data points, they train a network to generate intensity from other values. They train this network in an unsupervised manner.

**Geodesic Correlation Alignment**: This is introduce to correct the distribution differences at the end of the segmentation network between real and generated data. As for the Intensity rendering, this part is trained in an unsupervised manner.

**Progressive Domain Calibration**: Because shifts in the distribution at the beginning of the network will propagate up until the end, they change the outputs statistics of the network at the end of each layers and update the values of the batchnorm with them.

All the described effect are shown in the figure below:

## Results

They improve on all of their previous results. The following table shows the improvements when adding the modules on the segmentation task (real data):

| Car | Pedestrian | Cyclist | Average |
|:--:|:-:|:-:|:-:|
| SqueezeSeg | 64.6 | 21.8 | 25.1 | 37.2 |
| +BN | 71.6 | 15.2 | 25.4 | 37.4 |
| +BN+M | 70.0 | 17.1 | 32.3 | 39.8 |
| +BN+M+FL | 71.2 | 22.8 | 27.5 | 40.5 |
| +BN+M+FL+CAM | **73.2** | **27.8** | **33.6** | **44.9** |
| PointSeg | 67.4 | 19.2 | 32.7 | 39.8 |

The table below shows the improved results for the training on the generated data with their new pipeline:

|  | Car | Pedestrian |
|:-:|:-:|:-:|
| SQSG trained on GTA | 29.0 | - |
| SQSG trained on GTA-LiDAR | 30.0 | 2.1 |
| +LIR | 42.0 | 16.7 |
| +LIR+GCA | 48.2 | 18.2 |
| +LIR+GCA+PDC | 50.3 | 18.6 |
| +LIR+GCA+PDC+CAM | 57.4 | 23.5 |
| SQSG trained on KITTI w/o intensity | 57.1 | - |