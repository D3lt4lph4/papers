# Estimating Velocity Fields on a Freeway From Low-Resolution Videos

_last modified : 16-07-2019_

## General Information

- Title: Estimating Velocity Fields on a Freeway From Low-Resolution Videos
- Authors: Young Cho and John Rice
- Link: [article](https://ieeexplore.ieee.org/document/4019430)
- Date of first submission: Dec 2006
- Implementations:

## Brief

According to the article, most if not all the algorithms used for flow estimation rely on tracking. This can work for high or medium quality videos but not for low quality videos. They also explain that camera motion or shadows and occlusion can be a problem when trying to estimate the speed of a vehicle. These problems are exacerbated by the distance of the camera. This article presents a method to extract the medium speed in a given lane without tracking on low resolution videos. 

## How Does It Work

This is a three steps method:

- First an "intensity profile" of the target lane is created for each moment in time
- Then, the best matching pattern of the current intensity profile is looked for at time \(t + \tau\) and \(t - \tau\) using the L_1 norm
- Finally the speed estimate is estimated as the slope of the line connecting the two centers of the pair (the current pattern and the best matching one)

An example of the intensity profile for a given time is shown in following figure, we can see the picks corresponding to the cars.

![Intensity Profile](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/EstimatingVelocityFieldsFreewayLowResolution/intensity_profile.png "Intensity Profile")

An example of the intensity profile (pixel vs time) is shown in the following figure. The lines progression show the progress over time of one or more vehicles.

![Intensity Time Distance](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/EstimatingVelocityFieldsFreewayLowResolution/intensity_time_distance.png "Intensity Time Distance")

## Results

They used a 15 minutes video of a highway to evaluate their model. The camera used covers about one mile of distance and the baseline speed of the flows are calculated using inductive loops. There is no link in the article to the dataset.
The following table shows the mean and standard deviation on the different station of the road (position of the induction loops used to get the real average of the speed). They explain the variations in the article, and all in all the method seems to work correctly.

| Satation | East bound | West bound |
|:--------:|:----------:|:----------:|
| Station 3 | -1.8 (4.5) | -2.8 (3.2) |
| Station 4 | 1.9 (3.6) | -0.7 (2.7) |
| Station 5 | 4.9 (2.7) | 0.4 (3.5) |
