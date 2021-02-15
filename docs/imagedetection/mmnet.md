# Fast Object Detection in Compressed Video

_last modified : 15-02-2021_

## General Information

- Title: Fast Object Detection in Compressed Video
- Authors: Shiyao Wang, Hongchao Lu, Zhidong Deng
- Link: [article](https://arxiv.org/pdf/1811.11057.pdf)
- Date of first submission: 
- Implementations: 

## Brief

In this paper the authors do detection using the compression format of mpeg4-10. Up until now, (to the best of our knowledge) all the detectors on images either run a per frame detection, thus not taking into account the temporal information of the video, or use heavy computation to calculate a motion information and use it for detection.

In this article, the authors aim to use the information already in the h264 compression. During the compression, different type of frames are created, I-frames and P-frames (also B, but they are ignored for this article). The I-frames are the full image at a given time, not more than a snapshot of the video, the P-frames hold difference information between the previous I-frame and the frame when the P-frame was created.
They take advantage of this two type of frames to create the MMNet which uses high cost computation on the first frame, and reduce cost for the next ones.
Very short description of what it does, advantages, scientific locks, etc

## How Does It Work

The network can be divided into 3 parts, first the feature extraction, then the memory unit and finally the detection network. The whole pipeline for detection is shown in figure.

![alt text](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/mmnet/mmnet_network.png "Pipeline for the whole network.")

The Nfeat part is here to extract the features from the I-frame, i.e the full image. Then, the lstm part compute the motion information to get new feature maps at each time step of the image. Finally, prediction is made for each frame using the feature maps, the prediction is made with a R-FCN network.

## Results

There are two main information to get from their results, first the composition motion vectors, residual vectors, LSTM and second, the comparison with the state of the art methods.

The usage of motion vectors and LSTM is compared in the following table:

| method | res | res | res |
|:--:|:--:|:--:|:--:|
| MV+Res ? |  | X | X|
| LSTM ? | X |  | X |
| mAP(\%) | 66.3 | 70.3 | 72.1 |
| mAP(\%)(fast) | 27.7 | 38.5 | 44.2 |
| mAP(\%)(medium) | 68.2 | 71.2 | 72.0 |
| mAP(\%)(slow) | 82.6 | 83.5 | 83.6 |

The following figure shows the different results for the detection networks with video.

![alt text](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/mmnet/mmnet_results_comparison.png "Comparison of different networks, mAP vs time")
