# An algorithm to estimate mean vehicle speed from MPEG Skycam video

_last modified : 04-02-2020_

## General Information 

- Title: An algorithm to estimate mean vehicle speed from MPEG Skycam video

- Authors: Xiaodong Yu, Ping Xue, Lingyu Duan & Qi Tian
- Link: [article](https://link.springer.com/article/10.1007/s11042-006-0073-8)
- Date of first submission: 30 December 2006
- Implementations: None

## Brief

They propose a novel statistical model to estimate the mean speed of vehicle from the compressed MPEG video flux. They make of the motion vector to estimate the speed of the vehicles on each lanes of the road. They reach an accuracy up to 85 to 92% when using proper spatial and temporal processing. They do not provide with speed gains when using their method when compared to method fully decoding the video data.

## How Does It Work

In order to predict the mean speed of the vehicles, they use a four step pipeline:

- A MPEG parser to extract the motion vectors and DCT coefficients from the video
- A filter module to remove the unreliable motion vectors
- A mapping model to map the motion vectors from the 2D plane (image) to the 3D plane (ground plane)
- A module to estimate the mean vehicle speed

**MPEG Parser**: A simple parser, they extract the P frame and store them into a buffer along with the DCT coefficients and macro block types.

**Filter module**: They use 2 motion vector filters to remove the unreliable motion vectors: a spatial window filter (lane mask) and a texture filter. The texture filter is used to remove motin vectors in low texture macroblocks as they are less likely to contain vehicles.

**Mapping model**: A simple mapping model calibrated offline once per camera.

**Mean speed estimation**: To estimate the mean speed, they take the mean vehicle motion vector and divide by the period of time between the P-frame and its reference frame. They average this with all the motion vector as using one motion vector is not reliable enough (with small objects, a small error has a big impact).

## Results

They carry a thorough analysis of all the parameters of their method and show that one can reach a precision up to 92% for the estimation of the mean speed.
