#  Estimation and analysis of urban traffic flow 

_last modified : 31-03-2020_

## General Information (main fields described, non-exhaustive list)

- Title: Estimation and analysis of urban traffic flow 
- Authors: Joonsoo Lee ; Alan C. Bovik 
- Link: [article](https://ieeexplore.ieee.org/document/5413520)
- Date of first submission: 17 February 2010
- Implementations:

## Brief

**Problem:**: Recent traffic surveillence systems target complicated tasks. Here we focus on collection of traffic flow information. Currently, information is collected by magnetometers, we wish to use an other method (it is not specified why magnetometers are not satisfactory).

This paper describes a method to extract traffic flows from road  cameras. They show that statistical analysis can be performed on the extracted flow to detect change in the distribution of the traffic.

**Solution:** The authors propose to take advantage of the already deployed cameras to carry the task. They do not wish to use detection/tracking based method and chose to provide with a rough overview of traffic flow in scenes.

**Evaluated on:** Collect by the authors and not provided.

**Results:** They show they can follow change in traffic over an example.

## How Does It Work

Algorithm (none of the parameters are given):

- They compute traffic flows using the method proposed in this [paper](https://www.semanticscholar.org/paper/The-Robust-Estimation-of-Multiple-Motions%3A-and-Flow-Black-Anandan/eee90c038f43370a29b07e46f38dfe6527143a2c)
- They carry an average using a [trimmed mean filter](https://ieeexplore.ieee.org/document/1164247) to remove noise
- Apply threshold to select the positive results

Figure below shows examples of outputs of the algorithm:

![results](  "results")

## Results

Using KL divergence they manage to show augmentation of the distance when the traffic changes from low to high.