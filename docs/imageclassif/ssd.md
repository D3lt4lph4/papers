# SSD

## General Information

- Title: SSD: Single Shot MultiBox Detector
- Authors: Wei Liu, Dragomir Anguelov, Dumitru Erhan, Christian Szegedy, Scott Reed
- Link: [article](https://arxiv.org/abs/1512.02325)
- Date of first submission: 8 Dec 2015
- Implementations:
    - [Keras](https://github.com/rykov8/ssd_keras)
    - [Caffe](https://github.com/weiliu89/caffe/tree/ssd)

## Brief

The SSD is a one-shot detector midway between the YOLO classifier and OverFeat (closer to YOLO than to OverFeat). As for YOLO, the main improvement of this network is the one-shot pass.
At the time it was published its scoring was among the best in the PASCAL VOC challenge regarding both the mAP (72.1% mAP) and the number of fps (58) on a  Nvidia Titan X, beating the YOLO.

## How Does It Work

The basic idea is to use grids of various scale to predict the different boxes present in the image. The SSD outputs boxes for different grids and tells if there is (or isn't) an object in each box.

The following image, taken from the original paper, describes this:

![How Does It Work](https://github.com/D3lt4lph4/papers/blob/master/docs/images/imageclassif/ssd/ssd-classif-how.png?raw=true "SSD grid")

There are two grids shown, for each of those grids there is a number of pre-set boxes that can match the ground truth boxes (only a few are on the diagrams). The network tells for each box if it matches or not an object in the image (here two matches for the cat and one for the dog). The bigger the grid, the smaller the object detected is, this is how the SSD allows for multiple detection in one shot.
It is also to be noted that the boxes are regressed to add in precision.

## Results

- PASCAL VOC 2007:

| Method | data | mAP |
|--------|:----:|:---:|
|SSD300 | 07 | 68.0 |
|SSD300 | 07+12 | 74.3 |
|SSD300 | 07+12+COCO | 79.6 |
|SSD512 | 07 | 71.6 |
|SSD512 | 07+12 | 76.8 |
|SSD512 | 07+12+COCO | 81.6 |

- PASCAL VOC 2012:

| Method | data | mAP |
|--------|:----:|:---:|
| SSD300 | 07++12 | 72.4 |
| SSD300 | 07++12+COCO | 77.5 |
| SSD512 | 07++12 | 74.9 |
| SSD512 | 07++12+COCO | 80.0 |

## In Depth

### Architecture

The SSD can be cut down into two main parts, the feature extractor and the regressor/classifier. For the first part, the VGG-16 is used, then convolutional layers are added to create the grids used for the classification/prediction. The image below shows the architecture of the network :

![SSD network](https://github.com/D3lt4lph4/papers/blob/master/docs/images/imageclassif/ssd/ssd-network.png?raw=true "SSD Network")

As can be seen the network outputs 8732 boxes, we can separate the boxes in 6 groups, one per scale for the boxes inferred. Each group is supposed to detect different size objects, the closer we are from the VGG-16 the smaller the object.

For each group of boxes, the number are as follows:

- from conv4_3, 5776 boxes for a detection size around 0.1 of the original image size
- from conv7, 2166 boxes for a detection size around 0.2 of the original image size
- from conv8_2, 600 boxes for a detection size around 0.38 of the original image size
- from conv9_2, 150 boxes for a detection size around 0.56 of the original image size
- from conv10_2, 36 boxes for a detection size around 0.74 of the original image size
- from conv11_2, 4 boxes for a detection size around 0.92 of the original image size

To explain a bit the numbers in the diagram, and how using convolution, one can go from filter map to boxes, let's take an example, the boxes obtained from the layer conv_9_2. The grid is 5x5, for a total of 25 cells. For each cell 6 boxes will be predicted using a 3x3 convolution, so we have 3x3x6x4. In addition to that, for each box, we need to tell the class associated, thus we have 3x3x(6x(Classes+4)).

### Loss

The loss function is modified to fit the huge number of boxes. All the boxes are either matched to an object or to the background. Because of this matching strategy, there is a lot more of unmatched box than matched box. This creates an imbalance for the training which could get the network to predict all the boxes as background. That is why the loss function uses a maximum ratio between the matched and unmatched boxes.

## Warning

An important unspecified point, in the paper the bounding boxes are regressed, but in the implementation they are also divided by some term that is here to account as some kind of variance. One could see this as some kind of normalization to take into account the difference a person who would tag the data would make if tagging two times the same image.