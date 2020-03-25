# A Semi-Automatic 2D solution for Vehicle Speed Estimation from Monocular Videos

(will be updated by a git hook on commit)
_last modified : 25-03-2020_

## General Information

- Title: A Semi-Automatic 2D solution for Vehicle Speed Estimation from Monocular Videos
- Authors: Amit Kumar, Pirazh Khorramshahi, Wei-An Lin, Prithviraj Dhar, Jun-Cheng Chen and Rama Chellappa
- Link: [article](http://openaccess.thecvf.com/content_cvpr_2018_workshops/papers/w3/Kumar_A_Semi-Automatic_2D_CVPR_2018_paper.pdf)
- Date of first submission: Jun 1, 2018
- Implementations:
    [python](https://github.com/NVIDIAAICITYCHALLENGE/2018AICITY_Maryland)

## Brief

This paper presents a method to estimate vehicles speed on roadways from monocular videos. The main challenge they face comes from the automation of the calibration of the transform related to the camera. Depending on how the camera is oriented, the transformation used to go from the real world to the camera image plane will change. To solve this problem, they propose to estimate the a rectifying transformation using the vanishing points in the image and then to use a scaling factor to account for the non planar parts of the road.

Their method relies on a three steps pipeline, first the objects are detected, second they are tracked and finally the projection onto the real world space is done (followed by speed estimation).

They ranked seventh in the NVIDIA AI City challenge in 2018 and obtained a RMSE of 9.54 mph.

## How Does It Work

The three step pipeline used is shown in the image below.

![pipeline]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/Semiautomatic2dspeedestimationmonocular/pipeline.png "pipeline")

**Detections:** For the detection of the boxes, they use a Mask R-CNN. They choose this one because it is accurate and can detect vehicles at different scales.

**Tracking:** They test two different tracking algorithms, SORT and DeepSORT.

**Velocity Estimation:** The velocity estimation is a two steps pipeline. First an affine rectification is done and then a scale recovery. The affine rectification aims to undo the scales transformations induced by the representation of the real world in a planar image (set the roads straight with a correct scale). This affine transformation is based on the hypothesis that the road is planar, the scale recovery correct the error in case of a non planar road. Then the speed is estimated using the lenght of the white stripes on the road.


## Results

They evaluate on the NVIDIA AI City Challenge Dataset (2018). They compare their architecture with the two tracking methods, SORT and DeepSORT.

| Method | Detection Rate | RMSE |
|:-------|:---------------|:-----|
| SORT | 1.00 | 9.54 |
| DeepSORT | 1.00 | 10.10 |

They ranked 7th in the competition.