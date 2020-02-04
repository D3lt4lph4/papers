# Compressed-Domain Highway Vehicle Counting by Spatial and Temporal Regression

_last modified : 04-02-2020_

## General Information

- Title:  Compressed-Domain Highway Vehicle Counting by Spatial and Temporal Regression 
- Authors: Zilei Wang, Xu Liu, Jiashi Feng, Jian Yang, Hongsheng Xi
- Link: [article](https://ieeexplore.ieee.org/document/8064684)
- Date of first submission: 11 October 2017
- Implementations: 

## Brief

This article presents a method to count vehicles on highways. Contrary to other previous methods, they use the compressed representation of the data to estimate the number of vehicles. More specifically, they use H.264 compressed video as input, extract relevant predefined features, select a target regressor through classification and then regress the number of vehicles on the road. With this novel method, they obtain "similar performance with much lower computational cost". They claim to achieve 110 fps while previous methods were at about 10 fps.


## How Does It Work

The method used is a 4 steps method:

- video preprocessing
- feature extraction
- estimation with spatial regression
- refinement with temporal regression

These steps are shown in the following graphic:

![Extraction Pipeline](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/CompressedDomainHighwayVehicleCountingRegression/extraction_pipeline.png "Extraction Pipeline")

**Preprocessing**: The preprocessing step "include the motion vector normalization, macro-block weighting, foreground segmentation, and perspective normalization". Apart from the foreground segmentation, this steps can be seen as normalization of the importance of the motion vectors (one could argue that foreground segmentation is setting the importance to 0 for the background blocks).

**Feature extraction**: Various features (listed below) are extracted in this step, they will be used for the classification layer.

- Area: The number of blocks belonging to the segmented foreground
- Perimeter length: The total number of blocks lying on the perimeter of the foreground segment
- Shape: For a given segment, the shape is an orientation histogram of the perimeter blocks
- HOMV: Same as shape except that all the MV are used
- Texture: They use local binary pattern ([LBP](https://www.researchgate.net/publication/221047264_Advanced_Local_Binary_Pattern_Descriptors_for_Crowd_Estimation)) as features, more specifically [CS-LBP](https://www.sciencedirect.com/science/article/pii/S0031320308003282)

All of these hand crafted features are then used to estimate the number of vehicles on screen.

**Regressions**: Using the aforementioned features, they carry regressions to predict the number of cars on the screen. More specifically, a double classification is first carried to select the best train regressor for a given image. High, medium, low density of cars on the road for the first classifier and border classes for the second (the overlapping areas in the image below). Once the regressor is selected, the count is calculated and then, an estimated count is calculated through temporal regression (see image below).

![Regression Pipeline](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/CompressedDomainHighwayVehicleCountingRegression/regression.png "Regression Pipeline")


## Results

In all the test cases, their method did not manage to attain the state of the art, although they are not far from it. In the first of the tested dataset, they rank second in results. In the other one they are somewhere close to the third place.

Results on the UCSD dataset:

| Number of training samples | 200 | 300 | 400 | 500 | 600 | 700 | 800 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
 | Proposed Method | 2.963 | 2.923 | 2.868 | 2.775 | 2.687 | 2.525 | 2.446 |
 | Chanet al. | 4.140 | 3.581 | 3.439 | 3.415 | 3.229 | 3.020 | 2.970 |
 | Ryanet al. | 3.866 | 3.443 | 3.432 | 3.268 | 3.170 | 2.923 | 2.917 |
 | Counting CNN | 2.986 | 2.997 | 2.893 | 2.866 | 2.729 | 2.6822 | .634 |
 | Hydra 3s | 2.468 | 2.365 | 2.214 | 2.261 | 2.209 | 2.042 | 2.029 |

Resutls on the US101 dataset:

| Number of training samples | 600 | 700 | 800 | 900 | 1000 | 1100 | 1200 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| HCR-LOESS | 1.535 | 1.289 | 1.206 | 1.150 | 1.131 | 1.112 | 1.097 |
| Chanet al. | 1.589 | 1.331 | 1.212 | 1.153 | 1.124 | 1.115 | 1.086 |
| Ryanet al. | 1.551 | 1.317 | 1.209 | 1.146 | 1.124 | 1.113 | 1.058 |
| Counting CNN | 1.199 | 1.180 | 1.178 | 1.169 | 1.166 | 1.159 | 1.121 |
| Hydra 3s | 0.995 | 0.989 | 0.972 | 0.977 | 0.941 | 0.954 | 0.924 |
