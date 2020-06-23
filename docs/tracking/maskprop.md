# MaskProp (in progress)

_last modified : 23-06-2020_

## General Information

- Title: Classifying, Segmenting, and Tracking Object Instances in Video with Mask Propagation
- Authors: Gedas Bertasius, Lorenzo Torresani
- Link: [article](https://arxiv.org/abs/1912.04573)
- Date of first submission: 10 Dec 2019
- Implementations:

## Brief

**Problem:** In this article, the authors tackle the problem of video instance segmentation and tracking. Specifically they focus on simplifying the pipeline used by other state of the art methods while maintaining/improving robustness to motion blur and occlusions.

**Solution:** They propose "MaskProp" a modified MaskRCNN that uses the predictions at a given frame to predict object position in past and future frames. With this added information, they improve the quality of the tracking and segmentation.

**Evaluated on:** They evaluate their method on the YouTube-VIS dataset.

**Results:** They improve on the accuracy of the state of the art method by a few points, from 44.8 to 46.6, while at the same time requiring less labeled data (1000x fewer images and 10x fewer bounding-boxes)

## How Does It Work

The proposed method works in two steps:

- first the video is separated in overlapping clips (a clip is a collection of frames from time t - T to time t + T), for each of the clips, instances will be predicted
- Once all the clips have been processed, a matching algorithm (not learned) based on instance intersection over union is used to unify the matching clip instances into one instance.

The main contribution is in the first step, where the prediction occurs. The aim is to predict the segmentation of each instances in a clip. To predict the instances in a clip, first, a Mask R-CNN is run on the frame t. Then using the information from this frame and information from the frame at the time we want the prediction, the other instances' segmentation are predicted. This is shown in the figure below:

![image1]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/tracking/maskprop/mask_prop.png "image")

In order to use information from two frames, two feature tensors (one representing each frame) are concatenated. But as the objects move throughout the video, features corresponding to the same objects would not be aligned in the two tensors. To solve this problem, they use Deformable Convolutions which aim to align information from the reference tensor with the tensor at the time of prediction. This is shown in the following graphic:

![image2]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/tracking/maskprop/mask_prop_2.png "image 2")

For each of the predicted instances at time t:

- Instance Feature Computation: the feature tensor a time t is masked with the predicted target instance to only keep features theoretically describing the target instance
- Instance Feature Propagation: Subtraction between the tensors describing the frames allows to get movement information to compute the positions of the Deformable Convolutions
- Propageted Instance Segmentation: Using the concatenation of the reference feature tensor re-aligned with Deformable Convolutions and the tensor at target time, the new instance is predicted

## Results

They evaluate on the YouTube-VIS dataset and claim to be the best reported accuracy.

| Method | Pre-training Data | mAP | AP@75 | AR@1 | AR@10 |
|:-:|:-:|:-:|:-:|:-:|:-:|
| DeepSORT | Imagenet, COCO | 26.1 | 26.1 | 27.8 | 31.3 |
| FEELVOS | Imagenet, COCO | 26.9 | 29.7 | 29.9 | 33.4 |
| OSMN | Imagenet, COCO | 27.5 | 29.1 | 28.6 | 33.1 |
| MaskTrack R-CNN | Imagenet, COCO | 30.3 | 32.6 | 31.0 | 35.5 |
| MaskTrack R-CNN∗ | Imagenet, COCO | 36.9 | 40.2 | 34.3 | 42.9 |
| EnsembleVIS | Imagenet, COCO, Instagram, OpenImages | 44.8 | 48.9 | 42.7 | 51.7 |
| MaskProp | Imagenet, COCO | **46.6** | **51.2** | **44.0** | **52.6** |
