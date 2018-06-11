# FSSD

## General Information

- Title: FSSD: Feature Fusion Single Shot Multibox Detector
- Authors: Zuo-Xin Li, Fu-Qiang Zhou
- Link: [article](https://arxiv.org/pdf/1712.00960.pdf)
- Date of first submission: 4 December 2017
- Implementations:
    - [Pytorch](https://github.com/lzx1413/PytorchSSD)
    - [Caffe](https://github.com/lzx1413/CAFFE_SSD/tree/fssd)

## Brief

The FSSD is an improved version of the SSD. The authors try to add semantic information to improve the mAP, while at the same time not loose too much time in computation. 

## How Does It Work

The FSSD is very close to the SSD, the principle is exactly the same, a cascade of convolutional layers used to predict a set of boxes. The  difference is that the networks makes two passes on some layers to add information on the smaller boxes predicted (see image below):


<!--- \captionsource{SSD vs FSSD Networks}{https://arxiv.org/pdf/1712.00960.pdf} -->

## Results

The results shown here are the main results for the networks, some were omitted, look into the paper for more details.
<!---

        Model & train set & mAP & fps & gpu & backbone network \\
        \hline
        \textit{Faster RCNN} & 07+12 & 73.2 & 7 & Titan X & VGGNet \\
        \textit{Faster RCNN} & 07+12 & 76.2 & 2.4 & K40 & ResNet-101 \\
        \textit{SSD} & 07+12+COCO & 81.2 & 46 & Titan X & VGGNet \\
        \textit{SSD} & 07+12 & 77.2 & 85 & 1080Ti & VGGNet \\
        \textit{FSSD300} & 07+12+COCO & 82.7 & 65.8 & 1080Ti & VGGNet \\-->

Comparison of results for classification on the VOC 2007 test set.

## In Depth

Here, go full description, tricks and all, keep in mind this is to explain the paper, but still a summary.

## Warning

None so far.

