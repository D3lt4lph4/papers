# Algorithms for Calibrating Roadside Traffic Cameras and Estimating Mean Vehicle Speed

_last modified : 31-03-2020_

## General Information

- Title: Algorithms for Calibrating Roadside Traffic Cameras and Estimating Mean Vehicle Speed
- Authors:  Todd N. Schoepflin, Daniel J. Dailey 
- Link: [article](https://ieeexplore.ieee.org/document/4357806)
- Date of first submission: 22 October 2007 
- Implementations: 

## Brief

**Problem:** When using cameras for estimation of road parameters, the models needs to be calibrated to account for the changing angles respective to the road to each of the cameras. Moreover, the algorithms must work under various conditions (weather, illumination, ...) and low quality images (JPEG compression).

**Solution:** The authors present an algorithm that can automatically calibrate the parameters of the model depending on the camera and estimate the mean vehicle speed to make the overall results more robust to changing conditions.

**Evaluated on:** Source not specified. Highways recordings of surveillance cameras.

**Results:** No quantitative evaluation, we see resembling trends.

## How Does It Work

**Calibration of the camera:** The calibration of the camera is based on the lane markers of the road. They apply image processing operations to outline the markers, they resample to remove the non linearity due to perspective projection and use autocorrelation line per line to detect the markers. 


**Estimation of the mean vehicle speed:** Given a lane, pre-process the image, and apply cross-correlation to extract the average moving distance between to data points in time.

## Results

They compare induction loop results with their method. They find similar patterns between the predictions and the loop calculated signals. They evaluate at multiple times of the day and under different conditions. The method seems to be resilient to change in weather.
