# Compressed-Domain Highway Vehicle Counting by Spatial and Temporal Regression

_last modified : 23-01-2020_

## General Information (main fields described, non-exhaustive list)

- Title:  Compressed-Domain Highway Vehicle Counting by Spatial and Temporal Regression 
- Authors: Zilei Wang, Xu Liu, Jiashi Feng, Jian Yang, Hongsheng Xi
- Link: [article](https://ieeexplore.ieee.org/document/8064684)
- Date of first submission: 11 October 2017
- Implementations: 

## Brief

This article presents a method to count vehicles on highways. Contrary to other previous methods, they use the compressed representation of the data to estimate the number of vehicles. The data they use is in the H264 format and they use the motion vectors, manually extracted features and multi-regression to count the number of vehicles on screen. The main advantage of the method is the reduction of calculation power required to process the data.

The method they use is a 4 step method:

- video preprocessing
- feature extraction
- estimation with spatial regression
- refinement with temporal regression

With this novel method they almost reach the decompress format state of the art methods.

## How Does It Work

As said above, they use a 4 step method:

- video preprocessing
- feature extraction
- estimation with spatial regression
- refinement with temporal regression


## Results

Here put the results of the network, scores in competitions, ...

## In Depth

Here, go full description, tricks and all, keep in mind this is to explain the paper, but still a summary.