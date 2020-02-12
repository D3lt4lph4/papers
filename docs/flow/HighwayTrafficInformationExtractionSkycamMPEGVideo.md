# Highway Traffic Information Extraction from Skycam MPEG Video

_last modified : 12-02-2020_

## General Information (main fields described, non-exhaustive list)

- Title: Highway Traffic Information Extraction from Skycam MPEG Video
- Authors: Xiao-Dong Yu, Ling-Yu Dum, Qi Tian
- Link: [article](https://ieeexplore.ieee.org/document/1041185)
- Date of first submission:  6 Sept. 2002 
- Implementations:

## Brief

Vehicle speed and density are variables required for many ITS application. Usually one obtains them by using systems such as induction loops. An other way to do is by using road cameras and tracking algorithms. In this paper, the authors provide with a way of getting speed and density using the compressed video flux. The main advantage of this method is the gain is speed of execution. They also use skycams, which are cameras mounted at high altitude and thus with low resolution of the road.

They reach a 80-90% percent accuracy with their method.

## How Does It Work

The proposed solution is made of four modules:

- An MPEG parser to extract the DCT coefficients and the motion vectors
- Filters to remove the unreliable motion vectors
- Offline calibration of the camera
- Projection from image to ground plane to extract the information

**MPEG Parser**: They focus on the P frames for their method. The parser extract the information from the video flux without full decoding (smart usage of I frames to extract DCT blocks from the P frames).

**Filters**: They use 3 filters, direction, magnitude and texture. Direction and magnitude are cluster based filters to remove the outliers. The texture filters takes advantages of the fact that the road shows low textures and cars high textures to remove noise motion vectors.

**Offline Calibration**: They use the lane markers to obtain the point for calibrating the model to change from image to road plane.

**Projection and information extraction** They apply the previously calibrated model and then use the magnitude of the motion vectors to extract the speed of the vehicles. They then calculate a vehicle ration and match it with a class low, medium or high flow for density estimation.

## Results

They test their approach on three video clips of ten seconds each. They find their algorithm to work better in smooth condition than in heavy traffic. In the worst conditions, they get a maximum error of 20%.

