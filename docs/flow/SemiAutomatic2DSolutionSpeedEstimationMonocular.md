# A Semi-Automatic 2D solution forVehicle Speed Estimation from Monocular Videos

_last modified : 12-02-2020_

## General Information (main fields described, non-exhaustive list)

- Title: A Semi-Automatic 2D solution forVehicle Speed Estimation from Monocular Videos
- Authors: Amit Kumar, Pirazh Khorramshahi, Wei-An Lin, Prithviraj Dhar, Jun-Cheng Chen and Rama Chellappa
- Link: [article](http://openaccess.thecvf.com/content_cvpr_2018_workshops/papers/w3/Kumar_A_Semi-Automatic_2D_CVPR_2018_paper.pdf)
- Date of first submission: June 2018
- Implementations:

## Brief

This workshop paper was realized for the NVIDIA AI CITY Challenge. In this paper they address the estimation of speed for road vehicles from monocular videos. They act in a three module pipeline, detection, tracking and speed estimation.

The main contribution of this articles lies in algorithm they developed for transformation form the image domain to the ground place domain.

They ranked seven in the challenge, can detect all the cars in the videos and have a RMSE of 9.54 mph.

## How Does It Work

They used an estimation pipeline divided in three modules: detection, tracking and speed estimation. The whole pipeline is shown in the figure below:

![pipeline](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/SemiAutomatic2DSolutionSpeedEstimationMonocular/pipeline.png "pipeline")

**Vehicle detection**: They used MaskRCNN for the vehicle detection.

**Tracking**: They tested two algorithms for tracking, SORT and DeepSORT. The main difference between the two algorithm is the way they associate the detection for tracking, they do not rely on the same parameters. Ultimately SORT gave the best results.

**Speed Estimation**: They use a two step approach to estimate the speed, first they carry an affine rectification to parallelize the trajectories of the vehicles. Then they apply scale recovery to correctly estimate the speed depending on the distance to the camera.

## Results

They report the results for two tested tracking algorithms as well as their ranking in the competition (7th).

| Method | Detection Rate | RMSE |
|:-:|:-:|:-:|
| SORT | 1.00 | 9.54 |
| DeepSORT | 1.00 | 10.10 |
