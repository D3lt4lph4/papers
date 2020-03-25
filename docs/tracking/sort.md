# SORT

_last modified : 25-03-2020_

## General Information

- Title: SIMPLE ONLINE AND REALTIME TRACKING
- Authors: Alex Bewley, Zongyuan Ge, Lionel Ott, Fabio Ramos, Ben Upcroft
- Link: [article](https://arxiv.org/abs/1602.00763)
- Date of first submission: 2 Feb 2016
- Implementations:
    - [Python](https://github.com/abewley/sort)

## Brief

In this paper the authors tackle real-time object tracking. Most of the existing approach are either fast or accurate. The authors argue that this is due to task such as object re-identification which are too complexe for use in real-time. They propose a simple approach that does not account for corner cases but works extremely fast. The method is called SORT and is based on Kalman Filter and Hungarian algorithm. The mapproach achieves state-of-the-art accuracy while being able to update the tracker at a rate of 260 Hz (over 20x faster than other state-of-the-art methods).

## How Does It Work

The method is based on a four steps pipeline:

- First all the objects are detected in the image
- Second, existing tracks positions are updated using a Kalman filter
- Then, all the updated positions are matched to the detections using an Hungarian algorithm
- Finally, un-matched detection are set as new tracks

There are also some rules implemented to remove lost tracks and ignore noise detections.

## Results

They evaluate on MOT benchmark sequences. Hereafter is the graph detailing speed vs accuracy, they provide with a detailled table but do not present the update rate in it, check the paper for more details.

![results]( https://github.com/D3lt4lph4/papers/blob/master/docs/images/tracking/sort/results.png "results")