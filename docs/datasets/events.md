# Events dataset

_last modified : 19-07-2019_

This section regroups the dataset regarding event happening in an image/video such as aggression/accident/loading of an object/...

## VIRAT Video Dataset

"Dataset designed to be realistic, natural and challenging for video surveillance domains in terms of its resolution, background clutter, diversity in scenes, and human activity/event categories than existing action recognition datasets."

- Contains:
  - objects: 
    - persons
    - car
    - objects
  - events:
    - Person loading an Object to a Vehicle
    - Person Opening a Vehicle Trunk
    - Person getting into a Vehicle
    - Person digging
    - ...

- Size:
  - 2–30Hz frame rates and 10–200 pixels in person-height
  - 8.5 hours of HD videos
  - large number of examples (>30) per action class

- Article:
  - Title: A Large-scale Benchmark Dataset for Event Recognition in Surveillance Video
  - Authors:  Sangmin Oh, Anthony Hoogs, Amitha Perera, Naresh Cuntoor, Chia-Chih Chen, Jong Taek Lee, Saurajit Mukherjee, J.K. Aggarwal, Hyungtae Lee, Larry Davis, Eran Swears, Xiaoyang Wang, Qiang Ji, Kishore Reddy, Mubarak Shah, Carl Vondrick, Hamed Pirsiavash, Deva Ramanan, Jenny Yuen, Antonio Torralba, Bi Song, Anesco Fong, Amit Roy-Chowdhury, and Mita Desai
  - Link: [article](http://www.cs.columbia.edu/~vondrick/vatic/virat.pdf)


- Dataset: [here](http://www.viratdata.org/)

## The Procedural Human Action Videos (PHAV) Dataset

Generated dataset containing action made by/on humans.

- Contains:
  - accidents
  - shooting in a ball
  - couple walking
  - ...

- Size:
  - 39,982 videos that have been generated autonomously by a computer

- Article:
  - Title: Procedural Generation of Videos to Train Deep Action Recognition Networks
  - Authors: De Souza, C R and Gaidon, A and Cabon, Y and Lopez Pena, A M
  - Link: [article](https://arxiv.org/abs/1612.00881)

- Dataset: [here](http://academictorrents.com/collection/phav)

## The AVA Dataset

Contains human action extracted from various movies.

- Contains:
  - listen to
  - dance
  - bow
  - run
  - ...

- Size:
  - 80 atomic visual actions
  - 351k movie clips

- Article:
  - Title: AVA: A Video Dataset of Spatio-temporally Localized Atomic Visual Actions
  - Authors: Chunhui Gu, Chen Sun, David A. Ross, Carl Vondrick, Caroline Pantofaru, Yeqing Li, Sudheendra Vijayanarasimhan, George Toderici, Susanna Ricco, Rahul Sukthankar, Cordelia Schmid, Jitendra Malik
  - Link: [article](https://arxiv.org/abs/1705.08421)

- Dataset: [here](https://research.google.com/ava/index.html)

## The CAVIAR Test Case Scenarios

Dataset containing different scenarios of interest (people).

- Contains:
  - walking alone
  - meeting with others
  - window shopping
  - entering and exiting shops
  - fighting and passing out
  - leaving a package in a public place
  - ...

- Size:
  - resolution is half-resolution PAL standard (384 x 288 pixels, 25 frames per second) and compressed using MPEG2

- Dataset: [here](http://groups.inf.ed.ac.uk/vision/CAVIAR/CAVIARDATA1/)