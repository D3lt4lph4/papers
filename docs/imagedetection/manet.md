# Fully Motion-Aware Network for Video ObjectDetection

_last modified : 15-02-2021_

## General Information (main fields described, non-exhaustive list)

- Title: Fully Motion-Aware Network for Video ObjectDetection
- Authors: Shiyao Wang, Yucong Zhou, Junjie Yan, Zhidong Deng
- Link: [article](https://openaccess.thecvf.com/content_ECCV_2018/html/Shiyao_Wang_Fully_Motion-Aware_Network_ECCV_2018_paper.html)
- Date of first submission: 2018
- Implementations:

## Brief

This paper, \citep{Wang_2018_ECCV}, improves on detection of objects in videos. More precisely, it tries to solve the problem of the method used in the paper \citep{DBLP:journals/corr/ZhuWDYW17}. In this paper, they use pixel calibration to improve on the detection, making usage of the time variable in the videos.

To remove this problem, they propose to add instance calibration. The image \ref{manet:instance_calibration} shows the improvement one can get using instance calibration in addition to the previous methods.

![palceholder text](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/manet/manet_instance_calibration.png "Example of improvement with instance calibration.")


## How Does It Work

The network can be divided into three parts, $N_{feat}$ the feature extractor, $N_{rpm}$ the region proposal network, $N_{rfcn}$ the region based detector. This pipeline is very similar to the original R-FCN with the difference that multiple frames are aggregated to take into account the time component. The whole network is shown in figure.

![palceholder text](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/manet/manet_full_network.png "The overall framework of the proposed fully motion-aware network (MANet). It composes the four steps below: (a) single frame feature extraction and flow estimation whose results are fed to the next two steps; (b) the pixel-level calibration by per-pixel warping; (c) the instance-level calibration through predicting instance movements; (d) the motion pattern based feature combination.")

The blue step is for the pixel calibration, the p matrices are flow estimated matrices that are here to correct the position of each pixel in the input matrix. With this, a first set of filter, $s^i_{pixel}$. It should be noted that the features are averaged, not concatenated.

The the red step is instance calibration, here it is the instance that are moved as a whole, giving the output matrix $s^i_{insta}$. 

Finally, $s^i_{pixel}$ and $s^i_{insta}$ are merged to give the correct prediction for the objects in the image.

## Results

All the results obtained for this network are presented on the ImageNet VID dataset (\citet{DBLP:journals/corr/RussakovskyDSKSMHKKBBF14}). The table \ref{manet:results_ablation} shows the different mAP given the possible mix in the architectures. The table \ref{manet:results_comparison} shows the comparison between the state of the art networks.

| method | 1 |  1 |  1 |  1 |  1 | 
|:--:|:-:|:-:|:-:|:-:|:-:|
| multi-frame feature aggregation ? | | X | X | X | X |
| Pixel-level Calibration ? | | | X | | X |
| Instance-level Calibration ? | | | | X | X |
| mAP(\%) | 73.6 | 73.4 | 76.5 | 77.1 | 78.1 |
| mAP(\%)(fast) | 81.8 | 83.8 | 85.0 | 85.5 | 86.9 |
| mAP(\%)(medium) | 71.3 | 75.7 | 74.9 | 76.1 | 76.8 |
| mAP(\%)(slow) | 52.2 | 45.2 | 56.6 | 55.4 | 56.7 |



| Network | results |
|:-:|:-:|
| R-FCN | 73.6 |
| TPN+LSTM | 68.4 |
| D (\& T loss) | 75.8 |
| DFF | 72.8 |
| FGFA | 76.5 |
| MANet | **78.1** |
| TCN | 47.5 |
| TCNN | 73.8 |
| D (\& T loss)(tau= 1) | 79.8 |
| MANet(+ Seq-nms) | **80.3** |
