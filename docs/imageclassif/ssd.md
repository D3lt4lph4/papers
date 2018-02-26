# SSD

## General Information

- Title: SSD - Single Shot MultiBox Detector
- Authors: Wei Liu, Dragomir Anguelov, Dumitru Erhan, Christian Szegedy, Scott Reed
- Link: https://arxiv.org/abs/1512.02325
- Date of first submission: 8 Dec 2015
- Implementations: 
    - Keras: https://github.com/rykov8/ssd_keras
    - Caffe: https://github.com/weiliu89/caffe/tree/ssd
   
## Brief

The SSD output bounding boxes around the selection of objects to detect. It is part of the new
generation of classifiers (with YOLO) and improves the detection workflow by making the detection
in a single shot (as opposite with the previous networks, Fast R-CNN, Faster R-CNN).
At the time it was published its scoring was among the best in the PASCAL VOC challenge regarding both 
the mAP (72.1% mAP) and the number of fps (58) on a  Nvidia Titan X.

## How Does It Work ?

The basic idea is to use grids of various scale to predict the different boxes present in the image.
The following image, taken from the original paper, describes this:

![How Does It Work](https://github.com/D3lt4lph4/papers/blob/master/docs/images/imageclassif/ssd/ssd-classif-how.png?raw=true "SSD grid")

## In Depth

The SSD uses the VGG-16 as base classifier then adds its own layers to output the boxes. The image
below shows the architecture of the network : 

![SSD network](https://github.com/D3lt4lph4/papers/blob/master/docs/images/imageclassif/ssd/ssd-network.png?raw=true "SSD Network")

The network outputs 8732 boxes, we can separate the boxes in 6 groups, one for each layer the boxes are
inferred from. Each group is supposed to detect different size objects, the closer we are from the VGG-16
the smaller the object.
For each group of boxes, the number are as follow:
- from conv4_3, 5776 boxes for a detection size around 0.1 of the original image size
- from conv7, 2166 boxes for a detection size around 0.2 of the original image size
- from conv8_2, 600 boxes for a detection size around 0.38 of the original image size
- from conv9_2, 150 boxes for a detection size around 0.56 of the original image size
- from conv10_2, 36 boxes for a detection size around 0.74 of the original image size
- from conv11_2, 4 boxes for a detection size around 0.92 of the original image size
