# RCNN

_last modified : 01-09-2018_

## General Information

- Title: Rich feature hierarchies for accurate object detection and semantic segmentation
- Authors: Ross Girshick, Jeff Donahue, Trevor Darrell, Jitendra Malik
- Link: [article](https://arxiv.org/pdf/1311.2524.pdf)
- Date of first submission: 11 November 2013
- Implementations:
    - [Caffe](https://github.com/rbgirshick/rcnn)

## Brief

This network is one of the pioneers for object detection. In its conception it is tightly linked to the OverFeat network, as described in the article : "OverFeat can be seen (roughly) as a special case of R-CNN.".

Even if the architecture of the network is inspired by OverFeat, the RCNN outperformed all of the results at the time og its publication. 

One of the main contribution of the paper is to demonstrate the gain obtained when pre-training on large auxiliary dataset and after that training on the target set (usually smaller).

This is not an end-to-end classifier as we can see nowadays.

## How Does It Work

The network is made of three main parts, the region extractor, the feature extractor and finally the classifier. The whole network is shown in the following image:

![RCNN Network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/imagedetection/rcnn/rcnn_network.png "RCNN Network")

A region proposal algorithm extract ROI, then each region is fed to a classifier and finally the extracted features are classified.

## Results

The results are for two different dataset.

Results for the PASCAL VOC 2010 challenge :

| Model | mAP |
|-------|-----|
| RCNN | 53.7 |
| SegDPM | 40.4 |
| Regionlets | 39.7 |
| UVA | 35.1 |
| DPM v5 | 33.4 |

links :

- [DPM v5](https://www.rossgirshick.info/latent/)
- [UVA](https://ivi.fnwi.uva.nl/isis/publications/bibtexbrowser.php?key=UijlingsIJCV2013&bib=all.bib)
- [Regionlets](http://www.ece.northwestern.edu/~mya671/mypapers/ICCV13_Wang_Yang_Zhu_Lin.pdf)
- [SegDPM](https://www.cv-foundation.org/openaccess/content_cvpr_2013/papers/Fidler_Bottom-Up_Segmentation_for_2013_CVPR_paper.pdf)


Results for the ILSVRC 2013 challenge :

| Model | mAP |
|-------|-----|
| RCNN | 31.4 |
| OverFeat | 24.3 |

links:

- [OverFeat](https://arxiv.org/abs/1312.6229)


## In Depth

### At test time

The first part of the network uses the [selective search](https://ivi.fnwi.uva.nl/isis/publications/bibtexbrowser.php?key=UijlingsIJCV2013&bib=all.bib) to generate around 2k boxes of possible objects.

Then, second part of the network uses the network of the Krizhevsky et al to generate a  4096-dimensional feature vector from each boxes that were proposed. The vector is generated using five the convolutional layers. The input image is a 227x227 mean-subtracted wrapped RGD image.

Finally the correct class is extracted using a SVM and Non-Maximum suppression from all the boxes.

### At training time

The CNN is trained with the fully connected layers at the end modified to match the number of classes in the dataset. 

The network is first pre-trained "on a large auxiliary dataset (ILSVRC2012 classification) using image-level annotations only", with all the classes. Then after replacing the fully connected with a smaller one to match the number of class, the network is fine tuned.

Finally, once the CNN part has converged, the SVMs are trained.

The part still unclear to me is why use the SVM extractor instead of the usual fully connected layer. Probably small improvement in the results.

## Warning

None so far.