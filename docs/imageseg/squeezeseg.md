# SqueezeSeg:  Convolutional  Neural  Nets  with  Recurrent  CRF  forReal-Time  Road-Object  Segmentation  from  3D  LiDAR  Point  Cloud

_last modified : 11-07-2019_

## General Information

- Title: SqueezeSeg:  Convolutional  Neural  Nets  with  Recurrent  CRF  forReal-Time  Road-Object  Segmentation  from  3D  LiDAR  Point  Cloud
- Authors: Bichen Wu, Alvin Wan, Xiangyu Yue and Kurt Keutzer
- Link: [article](https://arxiv.org/abs/1710.07368)
- Date of first submission: 19 Oct 2017
- Implementations: 
    - [tensorflow](https://github.com/BichenWuUCB/SqueezeSeg)

## Brief

This article presents a method to segment lidar cloud points. They use CNN coupled with CRF to predict the class of the points in the LIDAR cloud. They also provide with the instance segmentation by adding classical clustering technique.

They train on the Kitti dataset, and, because of the lack of data, they also extract data from a generator, GTA V. Through the generated data, they improve the prediction results. In order to use the generated data, they also provide with some techniques to more closely match the distribution of the real data.

## How Does It Work

They use a 2D classification network to provide with the segmentation, because of that they need to change the representation of the data, to go from 3D point cloud to 2D image.
They go from carthesian to polar coordinate and then, they discretise the points in a grid with some define resolution in the zenith $\theta$ and azimuth $\phi$ angles.

- $\theta = arcsin \frac{z}{\sqrt{x^2 + y^2 + z^2}}$
- $\phi = arcsin \frac{y}{\sqrt{x^2 + y^2}}$

With this they obtain 5 channel images, made of the x, y, z coordinates, the intensity and the range of the point (distance). The whole process is describe in the following image:

![Conversion](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageseg/squeezeseg/projection.png "Conversion")

Then they use a typical CNN structure for the generation of the segmentation maps. The network is depicted in the picture below. They also add few layers to code the CRF part (refinement of the results). Finally they predict the instances using DBSCAN.

![Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageseg/squeezeseg/network.png "Network")

## Results

They carry multiple evaluation regarding segmentation performance, speed of inference and segmentation using the generated data. They show that their method works well for car object but as trouble with the pedestrians and the cyclists. They attribute these difficulties of predictions to the number and size of the objects.

Regarding the speed of inference, they can run their algorithm faster than the sampling speed of the Lidar sensor. 

And finally, using GTAV + Kitti improve the results while using GTAV only degrade the results.
