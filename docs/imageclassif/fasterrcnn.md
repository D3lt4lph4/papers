# Faster R-CNN

## General Information

- Title: Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks
- Authors: Shaoqing Ren, Kaiming He, Ross Girshick, and Jian Sun
- Link: [article](https://arxiv.org/abs/1506.01497)
- Date of first submission: 4 Jun 2015
- Implementations:
    - [TensorFlow](https://github.com/endernewton/tf-faster-rcnn)
    - [Caffe/Matlab](https://github.com/ShaoqingRen/faster_rcnn)
    - [Pytorch](https://github.com/jwyang/faster-rcnn.pytorch)

## Brief

At the time of the publication, most of the object detection networks were in at least two part, one to extract ROI from the image and the second to classify the extracted regions. This was one of the bottlenecks in order to speed up the detections. The Faster R-CNN (which is basically a better version of the Fast R-CNN network) remove this bottleneck by introducing a Region Proposal Network (RPN).
According to the paper, they achieve a frame rate of 5fps on a GPU with the VGG16 as base network, while have state-of-the-art scores.

## How Does It Work

The network is made up of three parts as shown is the following image (taken from the article).

![Network architecture](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/fasterrcnn/network.png "Faster R-CNN")

We can see three parts in this image:

- The first one is the "conv layers", used to extract the features out of the image.
- The second one is the RPN, used to generate the ROI that will be used by the classifier.
- The last one is the classifier (Fast R-CNN) which tells for each ROI if there is an object from the target classes in it.

Something important to notice is the fact that both the classifier and the RPN share the same weights for the extraction of the features. This was done to be able to do only a single pass on the image and avoid having two networks for the whole workflow.

This sharing of the weights means the training will be a bit different from a classical deep learning training workflow. Here they did an "alternative training", meaning they first train one of the two, then the other, then the first, then second and so on until the model converge to som point.

Still, their method use a sliding window in order to get the ROI not making this classifier a one-shot one.

## Results

The following tables describe the results of the network depending on the type of network and dataset used. For the data, "07" is for the VOC 2007 trainval, "07+12" is for the union set of VOC 2007 trainval and VOC 2012 trainval and COCO stands for the COCO dataset.

| method | # proposals | data | mAP (%) |
|--------|:-----------:|:----:|:-------:|
|RPN+VGG unshared | 300 | 07 | 68.5 |
|RPN+VGG, shared | 300 | 07 | 69.9 |
|RPN+VGG, shared | 300 | 07+12 | 73.2 |
|RPN+VGG, shared | 300 | COCO+07+12 | 78.8 |

The second table make use of the PASCAL VOC 2012 dataset as well. For the data, "07" means the VOC 2007 trainval, "07++12" means the union set of VOC 2007 trainval+test and VOC 2012 trainval and COCO stands for the COCO dataset.

| method | # proposals | data | mAP (%) |
|--------|:-----------:|:----:|:-------:|
| RPN+VGG, shared | 300 | 12 | 67.0 |
| RPN+VGG, shared | 300 | 07++12 | 70.4 |
| RPN+VGG, shared | 300 | COCO+07++12 | 75.9 |

The number of fps for the RPN + Fast R-CNN is 5.

More details on the results are given on the paper, these are the main ones.

## In Depth

Let's describe a bit more each block of the network, first the RPN.

### Region Proposal Network

The RPN is based upon a sliding window and anchor boxes, for each position of the window, k anchor box are output, telling if there is or not an object in them. The following image shows a sliding window and the anchors that would be output (the ks in the image is for the number of anchor box).

![Network anchors](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/fasterrcnn/anchor.png "Faster R-CNN anchor")


Their method use convolutional layers to output the anchor boxes, thus making the RPN translation invariant and at the same time reducing the number of weights used for the output. Finally, the anchors are build on a pyramid of anchor thus removing the need to re-scale the image to detect object of different size.