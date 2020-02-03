# SqueezeSeg: Convolutional Neural Nets with Recurrent CRF forReal-Time Road-Object Segmentation from 3D LiDAR Point Cloud

_last modified : 03-02-2020_

## General Information

- Title: SqueezeSeg:  Convolutional  Neural  Nets  with  Recurrent  CRF  forReal-Time  Road-Object  Segmentation  from  3D  LiDAR  Point  Cloud
- Authors: Bichen Wu, Alvin Wan, Xiangyu Yue and Kurt Keutzer
- Link: [article](https://arxiv.org/abs/1710.07368)
- Date of first submission: 19 Oct 2017
- Implementations: 
    - [tensorflow](https://github.com/BichenWuUCB/SqueezeSeg)

## Brief

This article presents a method to segment lidar cloud points. They use CNN coupled with [CRF](https://en.wikipedia.org/wiki/Conditional_random_field) to predict the class of the points in the LIDAR cloud. They also provide with the instance segmentation by adding classical clustering technique ([DBSCAN](https://en.wikipedia.org/wiki/DBSCAN) clustering).

Because annotation for LiDAR images is costly, they train on images extracted from a realistic driving generator (GTAV). They close the domain gap with statistical analysis/modification. And, they show that it is possible to improve the segmentation results using the generated data.

## How Does It Work

They use a 2D classification network to provide with the segmentation, because of that they need to change the representation of the data: from 3D point cloud to 2D image.
They go from cartesian to polar coordinate and then, they discretize the points in a grid with some define resolution in the zenith $\theta$ and azimuth $\phi$ angles.

- $\theta = arcsin \frac{z}{\sqrt{x^2 + y^2 + z^2}}$
- $\phi = arcsin \frac{y}{\sqrt{x^2 + y^2}}$

With this they obtain 5 channel images, made of :

- the x, y, z coordinates
- the intensity of the point
- the range of the point (distance). 

The whole process is describe in the following image:

![Conversion](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageseg/squeezeseg/projection.png "Conversion")

Then they use a typical FCN structure for the generation of the segmentation maps. The network is depicted in the picture below. They also add few layers to code the CRF part (refinement of the results, not shown here, c.f article). Finally they predict the instances using DBSCAN.

![Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageseg/squeezeseg/network.png "Network")

## Results

They carry multiple evaluation regarding segmentation performance, speed of inference and segmentation using the generated data. They show that their method works well for car object but as trouble with the pedestrians and the cyclists. They attribute these difficulties of predictions to the number and size of the objects. The results are shown in the table below (only IoU, check the article for more details).

|  | Class-level | Instance-level |
|--|:---:|:---:|
| Car w CRF | **64.6** | **59.5** | 
| Car w/o CRF | 60.9 | 56.7 |
| Pedestrian w CRF | 21.8 | 20.8 |
| Pedestrian w/o CRF | **22.8** | **21.7** |
| Cyclist w CRF | 25.1 | 20.6 |
| Cyclist w/o CRF | **26.4** | **21.7** |

Regarding the speed of inference, they can run their algorithm faster than the sampling speed of the Lidar sensor.

|  | Average runtime (ms) | Standard deviation |
|--|:---:|:--:|
| SqueezeSeg w/o CRF | 8.7 | 0.5 |
| SqueezeSeg | 13.5 | 0.8 |
| DBSCAN clustering | 27.3 | 45.8 |

And finally, using GTAV + Kitti improve the results when compared with Kitti only, while using GTAV only degrade the results.

|  | Class-level | Instance-level |
|--|:---:|:--:|
| KITTI | 57.1 | 53.0 |
| GTA | 29.0 | 28.2 |
| KITTI + GTA | 66.0 | 61.4 |