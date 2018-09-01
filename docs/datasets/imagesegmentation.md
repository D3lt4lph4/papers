# Datasets for image segmentation

_last modified : 01-09-2018_

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