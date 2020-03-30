# DeepSORT 

_last modified : 30-03-2020_

## General Information

- Title: Simple Online and Realtime Tracking with a Deep Association Metric
- Authors: Nicolai Wojke, Alex Bewley, Dietrich Paulus
- Link: [article](https://arxiv.org/abs/1703.07402)
- Date of first submission: (to have some idea on the "age" of the article)
- Implementations:
    - [Python](https://github.com/nwojke/deep_sort)

## Brief

This paper aims to improve the SORT performances using appearance information. The authors add a pre-trained deep learning network to provide with the appearance information.
Their method reduce the number of identity switches by 45% while running at 20Hz (40Hz ? the two numbers are given at two different places in the paper). As a comparison, SORT runs at 60Hz.

## How Does It Work

The method is based on a five steps pipeline:

- First all the objects are detected in the image
- Second, existing tracks positions are updated using a Kalman filter
- Then, they cluster the tracks by age (how long the tracks as not been associated with a detection) and run the Hungarian algorithm on each of the cluster in increasing age order
- All the remaining unmatched and unconfirmed tracks of age 1 are processed using the original SORT algorithm 
- Finally, un-matched detection are set as new tracks

The cost used for the first matching step is set as a combination of the Mahalanobis and the cosine distances. The Mahalanobis distance is used to incorporate motion information and the cosine distance is used to similarity between two objects. To wompute the cosine distance, the rely on a CNN to compute the appearance descriptors (no precision on to how to train the network, but weights are provided).

There are also some rules implemented to remove lost tracks and ignore noisy detections.

## Results

They present there results on the MOT16 challenge:

![results]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/tracking/deepsort/results.png "results")

- Multi-object tracking accuracy (MOTA): Summary of over-all tracking accuracy in terms of false positives, false nega-tives and identity switches 
- Multi-object tracking precision (MOTP): Summary of over-all tracking precision in terms of bounding box overlap be-tween ground-truth and reported location
- Mostly  tracked  (MT):  Percentage  of  ground-truth  tracks that have the same label for at least 80% of their life span.
- Mostly lost(ML): Percentage of ground-truth tracks that are tracked for at most 20% of their life span.
- Identity switches (ID): Number of times the reported iden-tity of a ground-truth track changes.
- Fragmentation (FM): Number of times a track is interrupted by a missing detection
