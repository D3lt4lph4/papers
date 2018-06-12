# Faster R-CNN

## General Information

- Title: Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks
- Authors: Shaoqing Ren, Kaiming He, Ross Girshick, and Jian Sun
- Link: [article](https://arxiv.org/abs/1506.01497)
- Date of first submission: 4 Jun 2015
- Implementations: (I just put a few, there are a lot of implementation even per framework, check on the web to find the best one)
    - [TensorFlow](https://github.com/endernewton/tf-faster-rcnn)
    - [Caffe/Matlab](https://github.com/ShaoqingRen/faster_rcnn)
    - [Pytorch](https://github.com/jwyang/faster-rcnn.pytorch)

## Brief

The Faster R-CNN is an improved version of the Fast R-CNN. The main amelioration of the network was to transform the region proposal network into a neural network to integrate it into the whole architecture. They achieve a frame rate of 5fps on a GPU with the VGG16 as base network, while having state-of-the-art scores.

## How Does It Work

The network is made up of three parts as shown is the following image (taken from the article).

![Network architecture](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/fasterrcnn/network.png "Faster R-CNN")

We can see three parts in this image:

- The first one is the "conv layers", used to extract the features out of the image.
- The second one is the RPN, used to generate the ROI that will be used by the classifier.
- The last one is the classifier (Fast R-CNN) which tells for each ROI if there is an object from the target classes in it.

Something important to notice is the fact that both the classifier and the RPN share the same weights for the extraction of the features. This was done to be able to do only a single pass on the image and avoid having two networks for the whole workflow.

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

The main difference for this network with the Fast R-CNN is in the Region Proposal Network. The first thing is that this RPN makes the whole model trainable end-to-end. But, the counter part to this advantage is that the sharing of the weights means the training will be a bit different from a classical deep learning training workflow. Here they did an "alternative training", meaning they first train one of the two, then the other, then the first, then second and so on until the model converge at some point.

### Region Proposal Network

The RPN is based upon a sliding window and anchor boxes, for each position of the window, k anchor box are output, telling if there is or not an object in them. The following image shows a sliding window and the anchors that would be output (the ks in the image is for the number of anchor box).

![Network anchors](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imageclassif/fasterrcnn/anchor.png "Faster R-CNN anchor")

This means that for each location on the grid, there is 4k outputs for the k boxes (coordinates for each box) and 2k output for the class (object or not object). 

Their method use convolutional layers to output the anchor boxes, thus making the RPN translation invariant and at the same time reducing the number of weights used for the output.

Finally, the anchors are build on a "pyramid of anchor", that is the anchor are at multiple scale, thus removing the need to re-scale the image to detect object of different size.

# Training the whole network

Since both the RPN and the classifier share layers, the training was modify to help converging faster.

They describe different method in the paper, only the one they used will be described here.

They used a 4 steps training:

- First they train the RPN (section 3.1.3 of the paper);
- Then they train the classifier using the RPN of the step 1 (no layer shared);
- The RPN is fine-tuned using the convolutional layers of the step 2;
- Finally the classifier is fine-tuned in the same way.


## Warnings

None so far.

