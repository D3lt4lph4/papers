# Scene Graph Generation From Images

_last modified : 05-09-2018_

## General Information

- Title: Scene Graph Generation from Images
- Authors: Satoshi Tsutsui, Manish Kumar
- Link: [article](http://vision.soic.indiana.edu/b657/sp2016/projects/stsutsui/paper.pdf)
- Date of first submission: 2016
- Implementations: See links in the paper

## Brief

This paper details two method to generate scene graphs from captions and detected objects in an image. The methods "focus on two questions: what are the characteristics of objects and what are the relations between these objects", see below.

![example](https://github.com/D3lt4lph4/papers/blob/master/docs/images/scenegraph/scenegraphgenerationfromimages/brief.png?raw=true "example")

## How Does It Work

### Generation from caption

This approach first generate a caption from the image using a previous work from (Vinyals, Toshev, Bengio, & Erhan, 2015) then using the work of  
(Schuster et al., 2015) they go from caption to scene graph.

### Generation from object detection

In this part, they did not complete the generation, they stopped at the attribute and relation extraction.

The idea is the following one, use the R-CNN to extract the bounding boxes from the image to parse. Then, two different networks are used, one for the generation of the attributes and one for the generation of the relations.

This figure from the paper explain the architecture:

![example](https://github.com/D3lt4lph4/papers/blob/master/docs/images/scenegraph/scenegraphgenerationfromimages/from_objects.png?raw=true "example")

## Results

Accuracies:

| | train | val | test |
|-|-------|-----|------|
|relations|0.326|0.320|0.317|
|attributes|0.325|0.310|0.314|

It is to be noted that predicted "is on" instead of "on" count as false in the results.