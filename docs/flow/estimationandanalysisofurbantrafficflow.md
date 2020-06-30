#  Estimation and analysis of urban traffic flow 

_last modified : 30-06-2020_

## General Information (main fields described, non-exhaustive list)

- Title: Estimation and analysis of urban traffic flow 
- Authors: Joonsoo Lee ; Alan C. Bovik 
- Link: [article](https://ieeexplore.ieee.org/document/5413520)
- Date of first submission: 17 February 2010
- Implementations:

## Brief

**Problem:** Recent traffic surveillence systems target complicated tasks. Here we focus on estimation of traffic flow information. Currently, data is collected by magnetometers, they want to use other sensors to collect this information (it is not specified why magnetometers are not satisfactory).

**Solution:** The authors propose to take advantage of the already deployed cameras to carry the task. They do not wish to use detection/tracking based method and chose to use optical flow to estimate traffic flow descriptors.

**Evaluated on:** A dataset collected by the authors and not provided.

**Results:** They show they can follow change in traffic over an example.

## How Does It Work

The aim is to extract statistical information about the traffic flow using optical flow information. The first part of the method is to extract the optical flow from the images, the used algorithm is given below:

- They compute traffic flows using the method proposed in this [paper](https://www.semanticscholar.org/paper/The-Robust-Estimation-of-Multiple-Motions%3A-and-Flow-Black-Anandan/eee90c038f43370a29b07e46f38dfe6527143a2c)
- They carry an average using a [trimmed mean filter](https://ieeexplore.ieee.org/document/1164247) to remove noise
- Apply threshold to select the positive results

Figure below shows examples of outputs of the algorithm:

![results]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/estimationandanalysisofurbantrafficflow/results.png "results")

Then they compute histogram and derivatives of traffic flow vectors to be used a prior information of traffic flow.

## Results

They test their method for flow anomaly detection. They use previously computed histogram of a scene to detect changes in new histograms. They use a KL divergence they manage to show augmentation of the KL divergence when the traffic changes from low to high.
