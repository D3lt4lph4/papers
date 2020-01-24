# City-Wide Traffic Flow Estimation From a Limited Number of Low-Quality Cameras

_last modified : 11-07-2019_

## General Information

- Title: City-Wide Traffic Flow Estimation From a Limited Number of Low-Quality Cameras
- Authors: Tsuyoshi Idé, Takayuki Katsuki, Tetsuro Morimura, and Robert Morris
- Link: [article](https://ieeexplore.ieee.org/document/7547326)
- Date of first submission: 18 August 2016
- Implementations: None

## Brief

This article present two algorithms to estimate the traffic flow from low quality cameras. The first algorithm counts the number of vehicle from low-quality images. And the second estimate the traffic flow on a road section without cameras (c.f figure below).

![Problem](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/CityWideFlowEstimationLimitedCameras/problem.png "Problem")

The presented algorithms tackle three main challenges:

- Prediction on low quality cameras
- Elimination of the camera-wise calibration step
- Derive city-wide information from a limited number of webcams

They validate the presented method on two datasets, one taken in Nairobi, Kenya and the other taken in Kyoto, Japan.

## How Does It Work

**Counting the number of vehicles on screen:** The first part of the work concern the counting of vehicles. To realise this task, they operate in two steps:

- Extracting a variable x depending on the number of pixel above a threshold on screen (c.f image below)
- Estimate the number of vehicles using a Gaussian mixture model

![feature_extraction](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/CityWideFlowEstimationLimitedCameras/feature_extraction.png "feature extraction")

**Estimating the number of vehicles in an unseen part of the network:** In order to estimate the number of vehicles in part of the network without cameras, they 


## Results

Here put the results of the network, scores in competitions, ...
