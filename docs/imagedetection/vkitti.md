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

This article presents a new approach to deep learning training. They use generated data to train neural networks. They have four contributions:

- Generation of a generated dataset from an existing one
- Creation of the Virtual Kitti dataset
- Quantitative measure of the usefulness of the created world
- Measurement of the impact of weather condition on real datasets

## How Does It Work

The generation of the virtual world and evaluation of the usefulness follows a five steps scheme:

- Acquisition of the real data
- CLoning of the world (using the annotated real images and manual reconstruction of the world)
- Generation of various weather conditions
- Automatic generation of detailed ground truth annotations (notably segmentation, easier using virtual world)
- Evaluation of the "usefulness" of the world

## Results

Here put the results of the network, scores in competitions, ...

## In Depth

Here, go full description, tricks and all, keep in mind this is to explain the paper, but still a summary. Simply remove if the better solution is to read the paper.