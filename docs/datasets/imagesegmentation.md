# Datasets for image segmentation

_last modified : 03-01-2019_

Here are listed all the datasets that can be used for image segmentation. Each dataset should come with a small description of its size, what's in it and who provided it.

## The Berkeley BBD100K

- Contains:
    - Vehicles: Bus, Light, Sign, Person, Bike, Truck, Motor, Car, Train, Rider
    - Weather: clear, partly cloudy, over-cast, rainy, snowy, foggy, dawn/dusk, daytime, night
    - Different level of occlusion
    - Segmentation
    - Different scenes, such as: residential, highway, city, street, ...
    - Lane marking

- Size:
    - 100,000 HD video sequences of over 1,100-hour driving experience;
    - 2D Bounding Boxes annotated on 100,000 images;
    - Segmentation over 10,000 diverse images with pixel-level and rich instance-level annotations;
    - Multiple types of lane marking annotations on 100,000 images.

- Other details:
    - location: Different location in the USA, New York, Berkeley, San Francisco

- Article:
    - Authors: Fisher Yu, Wenqi Xian, Yingying Chen, Fangchen Liu, Mike Liao, Vashisht Madhavan, Trevor Darrell
    - Link: [article](https://arxiv.org/pdf/1805.04687.pdf)

- Dataset: [here](http://bdd-data.berkeley.edu/)

## Cityscapes Dataset

- Contains:
    - flat:	road, sidewalk, parking, rail track
    - human: person, rider
    - vehicle: car, truck, bus, on rails, motorcycle, bicycle, caravan, trailer
    - construction:	building, wall, fence, guard rail, bridge, tunnel
    - object: pole, pole group, traffic sign, traffic light
    - nature: vegetation, terrain
    - sky: sky
    - void: ground, dynamic, static

- Size:
    - 5 000 annotated images with fine annotations
    - 20 000 annotated images with coarse annotations

- Other details:
    - 50 cities
    - Several months (spring, summer, fall)
    - Daytime
    - Good/medium weather conditions
    - Manually selected frames:
        - Large number of dynamic objects
        - Varying scene layout
        - Varying background


- Article:
    - Authors: Marius Cordts, Mohamed Omran, Sebastian Ramos, Timo Rehfeld, Markus Enzweiler, Rodrigo Benenson, Uwe Franke, Stefan Roth, Bernt Schiele
    - Link: [article](https://arxiv.org/pdf/1604.01685.pdf)

- Dataset: [here](https://www.cityscapes-dataset.com/)

## The NYU Dataset

- Contains:
    - different rooms such as: Basements, Bedrooms, Home Offices, Bathrooms, ...

- Size:
    - 1449 densely labeled pairs of aligned RGB and depth images
    - 464 new scenes taken from 3 cities
    - 26 scene types
    - 407,024 new unlabeled frames
    - 1000+ Classes
    - Inpainted and raw depth available
    - Both object and instance labels

- Article:
    - Authors: Nathan Silberman, Pushmeet Kohli, Derek Hoiem, Rob Fergus
    - Link: [article](https://arxiv.org/pdf/1604.01685.pdfhttps://cs.nyu.edu/~silberman/papers/indoor_seg_support.pdf)

- Dataset: [here](https://cs.nyu.edu/~silberman/datasets/nyu_depth_v2.html)

## Appoloscape

- Contains:
	- Others others, rover
    - Sky: sky
    - Movable Object: car, car_groups, motorbicycle, motorbicycle_group, bicycle, bicycle_group, person, person_group, rider, rider_group, truck, truck_group, bus, bus_group, tricycle, tricycle_group
    - Flat: road, siderwalk
    - Road obstacles: traffic_cone, road_pile, fence
    - Roadside objects: traffic_light
    - Void: pole, traffic_sign, wall, dustbin, billboard
    - Building: building, bridge, tunnel, overpass
    - Natural: vegatation


- Size:
    - It is expected that the released dataset will include 200K image frames
    - On April 03, 2018，the Scene Parsing data set cumulatively provides 146,997 frames

- Other details:
    - Resolution: 3384 x 2710
    - Other: pixel-level annotations and pose information，depth maps

- Article:
    - Authors: Xinyu Huang, Peng Wang, Xinjing Cheng, Dingfu Zhou, Qichuan Geng, Ruigang Yang
    - Link: [article](https://arxiv.org/abs/1803.06184)

- Dataset: [here](http://apolloscape.auto/index.html)