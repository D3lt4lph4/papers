# Virtual Worlds as Proxy for Multi-Object Tracking Analysis

(will be updated by a git hook on commit)
_last modified : 11-07-2019_

## General Information (main fields described, non-exhaustive list)

- Title: Virtual Worlds as Proxy for Multi-Object Tracking Analysis
- Authors: Adrien Gaidon, Qiao Wang, Yohann Cabon and Eleonora Vig
- Link: [article](https://arxiv.org/abs/1605.06457)
- Date of first submission: 20 May 2016
- Implementations: 

## Brief

This article presents a new approach to deep learning training. They use generated data to train neural networks and show the impact of weather condition on real dataset. They have four contributions:

- Generation of a generated dataset from an existing one
- Creation of the Virtual Kitti dataset
- Quantitative measure of the usefulness of the created world for multi-object tracking
- Measurement of the impact of altered conditions on real datasets

## How Does It Work

The generation of the virtual world and evaluation of the usefulness follows a five steps scheme:

- Acquisition of the real data
- Cloning of the world (using the annotated real images and manual reconstruction of the world)
- Generation of various weather conditions
- Automatic generation of detailed ground truth annotations (notably segmentation, easier using virtual world)
- Evaluation of the usefulness by comparing the results obtained on real videos and the cloned ones (network trained on real data)

The measurement of the impact of altered conditions on real datasets is done by evaluating trained methods on generated altered synthetic data (angle change, rain, fog, ...) and comparing with synthetic unaltered images.

## Results

They show that networks trained on real data transfers quite well to synthetic videos. But conversely, network trained on synthetic data do not transfer to real video that well (see article for more details). The table below shows the results obtain on real videos and their clones.

| MDP | MOTA | MOTP | MT | ML | I | F | P | R |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0001 | 81.8% | 85.3% | 78.7% | 13.3% | 5 | 6 | 91.1% | 92.5% | 
| v0001 | 82.8% | 81.9% | 63.3% | 13.9% | 1 | 10 | 98.7% | 85.8% |
| 0002 | 80.7% | 82.2% | 63.6% | 27.3% | 0 | 1 | 99.0% | 82.5% |
| v0002 | 81.1% | 81.8% | 60.0% | 20.0% | 0 | 2 | 98.4% | 83.4% |
| 0006 | 91.3% | 84.3% | 72.7% | 9.1% | 0 | 3 | 99.7% | 92.3% |
| v0006 | 91.3% | 84.4% | 81.8% | 9.1% | 1 | 2 | 99.9% | 92.0% |
| 0018 | 91.1% | 87.0% | 52.9% | 35.3% | 1 | 1 | 96.7% | 95.2% |
| v0018 | 90.9% | 74.9% | 44.4% | 33.3% | 0 | 0 | 99.1% | 92.4% |
| 0020 | 84.4% | 85.1% | 58.1% | 25.6% | 14 | 24 | 96.7% | 88.7% |
| v0020 | 84.0% | 79.4% | 52.1% | 34.4% | 1 | 9 | 99.3% | 85.6% |
| AVG | 85.9% | 84.8% | 65.2% | 22.1% | 4 | 7 | 96.7% | 90.3% |
| v-AVG | 86.0% | 80.5% | 60.3% | 22.1% | 0 | 4 | 99.1% | 87.9% |

They also show strong degradation of the results when using altered conditions. Which suggest that the results obtained on the Kitti dataset may not work so well on other meteorological conditions.
