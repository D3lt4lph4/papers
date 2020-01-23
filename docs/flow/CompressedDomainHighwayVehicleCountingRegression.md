# Compressed-Domain Highway Vehicle Counting by Spatial and Temporal Regression

_last modified : 23-01-2020_

## General Information (main fields described, non-exhaustive list)

- Title:  Compressed-Domain Highway Vehicle Counting by Spatial and Temporal Regression 
- Authors: Zilei Wang, Xu Liu, Jiashi Feng, Jian Yang, Hongsheng Xi
- Link: [article](https://ieeexplore.ieee.org/document/8064684)
- Date of first submission: 11 October 2017
- Implementations: 

## Brief

This article presents a method to count vehicles on highways. Contrary to other previous methods, they use the compressed representation of the data to estimate the number of vehicles. More specifically, they use H.264 compressed video as input data, extract relevant predefined features and classify and then regress the number of vehicles on the road. With this novel method, they obtain "similar performance with much lower computational cost". The gain with this method is not specified in the paper.


## How Does It Work

The method used is a 4 steps method:

- video preprocessing
- feature extraction
- estimation with spatial regression
- refinement with temporal regression

These steps are shown in the following graphic:

![Extraction Pipeline](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/CompressedDomainHighwayVehicleCountingRegression/extraction_pipeline.png "Extraction Pipeline")

**Preprocessing**: The preprocessing step mostly standardize the data for the feature extraction.

**Feature extraction**: Various features (listed bellow) are extracted in this step, they will be used for the classification layer.

- Area: The number of blocks belonging to the segmented foreground
- Perimeter length: The total number of blocks lying on the perimeter of the foreground segment
- Shape: For a given segment, the shape is an orientation histogram of the perimeter blocks
- HOMV: Same as shape except that all the MV are used
- Texture: They use local binary pattern ([LBP](https://www.researchgate.net/publication/221047264_Advanced_Local_Binary_Pattern_Descriptors_for_Crowd_Estimation)) as features, more specifically [CS-LBP](https://www.sciencedirect.com/science/article/pii/S0031320308003282)

All of these hand crafted features are then used to estimate the number of vehicles on screen.

**Regressions**: Using the aforementioned features, they carry regressions to predict the number of cars on the screen. More specifically, a double classification is first carried to select the best train regressor for a given image (high, medium, low density for the first classifier and border  classes for the second). Once the regressor is selected, the count is calculated and then, an estimated count is calculated through temporal regression (see image bellow).

![Regression Pipeline](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/CompressedDomainHighwayVehicleCountingRegression/regression.png "Regression Pipeline")


## Results

In all the test cases, their method did not manage to attain the state of the art, although they are not far from it. In the first of the tested dataset, they rank second in results. In the other one they are somewhere close to the third place.
