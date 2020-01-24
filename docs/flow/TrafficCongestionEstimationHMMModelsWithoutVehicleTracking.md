# Traffic Congestion Estimation Using HMM Models Without Vehicle Tracking

_last modified : 11-07-2019_

## General Information

- Title: Traffic Congestion Estimation Using HMM Models Without Vehicle Tracking
- Authors: Fatih Porikli and Xiaokun Li
- Link: [article](https://ieeexplore.ieee.org/document/1336379)
- Date of first submission: 08 October 2004
- Implementations: None

## Brief

They train a low-latency traffic congestion estimation algorithm that uses MPEG images as inputs. They claim the algorithms to be unsupervised but later train on hand annotated data. They use hand crafted feature in combination with a Gaussian Mixture Hidden Markov Models to detect the five target traffic conditions (empty, open flow, mild congestion, heavy congestion,
and stopped).

They claim the 5 following advantages over other methods:

- High precision (95%)
- Low computational cost
- Very agile and low latency (2 seconds)
- Robust toward illumination changes
- Invariant to different camera setups

## How Does It Work

As a preprocessing step, they start by applying a mean filter to remove marginal values. Then, they set ROIs for each of the target traffic lanes, and, for each of the ROI they extract a feature vector made of seven features:

- Residues of DC components (density and speed of traffic (applied on I frames))
- Residues of AC components (similar to DC)
- Mean of the motion vectors (speed representation)
- Variance of the motion vectors (speed representation)
- The number of MV's into three magnitude bands: high, middle, low (distribution of the speed within the lanes)

Then these vectors are used to train 5 GM-HMMs that are used to predict the traffic event (with the Trillis (or [Viterbi](https://en.wikipedia.org/wiki/Viterbi_algorithm)) algorithm unlikely series of event are corrected). They also output a confidence score for the event prediction using the distance between the most likely event and the second most likely.

## Results

They evaluate on a dataset that includes various illumination conditions (sunny, overcast, dark, nighttime). The dataset contains 600 minutes of video.
The figure below show the predictions for about 33 minutes of videos (4000 GOP).

![results](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/TrafficCongestionEstimationHMMModelsWithoutVehicleTracking/results.png "results")

Using the filtered results, they have an accuracy rate of 97%.

