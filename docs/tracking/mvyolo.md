# MV-YOLO: Motion Vector-aided Tracking by Semantic Object Detection

_last modified : 15-02-2021_

## General Information

- Title: MV-YOLO: Motion Vector-aided Tracking by Semantic Object Detection
- Authors: Saeed Ranjbar Alvar, Ivan V. Bajić
- Link: [article](https://arxiv.org/abs/1805.00107)
- Date of first submission: 30 Apr 2018
- Implementations:

## Brief

In this paper, the authors present a work that aims to track object in videos using the compressed representation of the data. They exploit the motion vectors from the MPEG compressed videos to predict the position of detected objects.

They propose a method based on the hybrid usage of the motion vectors and fully decoded I-frames. They detect the objects in the pixel domain and carry the tracking in the motion vectors domain.

They show accuracy matching the recent trackers based on deep models. They can process images at 28 FPS.

## How Does It Work

They use a 3 part pipeline:

- Detection of the objects in the decoded frame
- Approximation of the target object position in the motion vector domain
- Prediction of the position using the detected objects as well as the motion vectors

The whole pipeline is shown in the picture below:


![network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/FlowNet/network.png "network")

**Detection of the objects**: For the detection of the objects they use different version of YOLO. The selection of the solution is a trade between precision and speed.

![network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/FlowNet/network.png "network")


## Results

Here put the results of the network, scores in competitions, ...