# An Algorithm to Estimate Vehicle Speed Using Un-Calibrated Cameras

_last modified : 31-03-2020_

## General Information

- Title: An Algorithm to Estimate Vehicle Speed Using Un-Calibrated Cameras
- Authors: ...
- Link: [article](link to the paper)
- Date of first submission: (to have some idea on the "age" of the article)
- Implementations: (if any found)
    - [Keras](http://awesomelink1)
    - [Caffe](http://awesomelink2)

## Brief

**Problem:** Estimating speed from uncalibrated camera is a not yet solved challenge. The existing solution all require the action of the operator to carry some calibration of the camera. In this article, we suppose that we do not have access to any information about the cameras (which can move).

**Solution:** The authors assert that exact calibration is not required for speed estimation and propose to use geometric relationships, "common sense" assumptions and the distribution of the vehicles lenght to solve the problem at hand.

**Evaluated on:** Not specified

**Results:** Up to 30% error

## How Does It Work

They present an algorithm not detailled here, which follows mostly the five following steps:

- obtain sequential images
- identify the moving vehicles in the sequential images
- track the vehicles between images
- dinamically estimate the scale factor in feet per pixel
- estimate speed from distance travelled and the interframe delay

## Results

Here put the results of the network, scores in competitions, ...