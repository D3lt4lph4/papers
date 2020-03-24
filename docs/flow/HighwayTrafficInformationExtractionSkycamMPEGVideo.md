# Highway Traffic Information Extraction from Skycam MPEG Video

_last modified : 24-03-2020_

## General Information (main fields described, non-exhaustive list)

- Title: Highway Traffic Information Extraction from Skycam MPEG Video
- Authors: Xiao-Dong Yu, Ling-Yu Dum, Qi Tian
- Link: [article](https://ieeexplore.ieee.org/document/1041185)
- Date of first submission:  6 Sept. 2002 
- Implementations:

## Brief

Vehicle speed and density are variables required for many ITS application. Usually one obtains them by using methods that either rely on close-view cameras or systems such as induction loops.

In this paper, the authors take another approach and provide with a way to use skycams (skycams are long range cameras onto which classical methods cannot be used). They propose a novel algorithm operating in the compressed MPEG domain that does not require training.

The advantages of using such a system are as follow:

- fast (decompression is skipped)
- require less material for deployment (a skycam cover a large portion of the road)

They reach a 80-90% percent accuracy with their method, depending on the traffic, i.e low, medium or high.

## How Does It Work

They use the motion vectors encoded within the video to estimate the speed and density of the vehicles on the road. The core of their method relies on the fact that in the frequency domain, vehicles tend to have high frequencies and roads low. Hence they can filter out noise motion vectors that are associated with roads.

The proposed solution is made of four modules (c.f figure below):

- An MPEG parser to extract the DCT coefficients and the motion vectors
- Filters in the DCT domain to remove the unreliable motion vectors, i.e the road (low frequency)
- Offline calibration of the camera
- Projection from image to ground plane to extract the information

![solution](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/HighwayTrafficInformationExtractionSkycamMPEGVideo/solution.png "solution")


**MPEG Parser**: They focus on the P frames for their method. The parser extract the information from the video flux without full decoding (smart usage of I frames to extract DCT blocks from the P frames).

**Filters**: They use 3 filters, direction, magnitude and texture. Direction and magnitude are cluster based filters to remove the outliers. The texture filters takes advantages of the fact that the road shows low textures and cars high textures to remove motion vectors associated with road segments.

**Offline Calibration**: They use lane markers to obtain the point for calibrating the model to change from image to road plane.

**Projection and information extraction** They apply the previously calibrated model and then use the magnitude of the motion vectors to extract the speed of the vehicles. They calculate a ratio with the motion vector remaining after filtering and the total before filter to obtain an estimate of traffic density: low, medium or high flow.

## Results

They test their approach on three video clips of ten seconds each. They find their algorithm to work better in smooth condition than in heavy traffic. In the worst conditions, they get a maximum error of 20%.
