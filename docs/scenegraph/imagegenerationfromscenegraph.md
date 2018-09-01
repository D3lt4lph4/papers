# Image Generation from Scene Graph

## General Information

- Title: Image Generation from Scene Graph
- Authors: Justin Johnson, Agrim Gupta and Li Fei-Fei
- Link: [article](https://arxiv.org/abs/1804.01622)
- Date of first submission: 4 April 2018
- Implementations:
    - [Python](https://github.com/google/sg2im)

## Brief

This article aims to take a sentence describing a scene, and generate an image from this description. It differs from previous work in the fact that a scene graph with relation between the object is processed instead of processing directly the sentence. No insight is given as to how generate the scene graph as an input.

## How Does It Work

The network works in two main parts, the first one processes the graph and allow for changing in space for the features in the graph. The second part takes the modified graph to generate the images.

This image from the articles shows the whole pipeline:

![network pipeline](https://github.com/D3lt4lph4/papers/blob/master/docs/images/scenegraph/imagegenerationfromscenegraph/pipeline.png?raw=true "Network Pipeline")

The scene graph is transformed while keeping the same graph structure, then the boxes and shapes are predicted and finally, the image is generated.

## Results

The network was tested on two dataset, COCO-stuff and Visual Genome. The results are in the range of the other method compared to ([StackGAN](https://arxiv.org/abs/1612.03242)). There was also a study realized with real person as judges, and it seems that this method produce images closer to what a human would understand.

## In Depth

Let's describe a bit more each steps of the network.

First there is the graph with the object and their relation between each one of them. The graph is a list of tuples ($o_i$ ,r ,$o_j$), all the object are linked to an other one.

From this graph there is a "one to one" mapping with graph convolutions as describe in the following image:

![graph to graph](https://github.com/D3lt4lph4/papers/blob/master/docs/images/scenegraph/imagegenerationfromscenegraph/graph_to_graph.png?raw=true "Graph to Graph")

When one go from $v_r$ to $v'_r$ the function only use the input relation and the to objects target of this relation. But when you go from object to object, all the relation linking this object to other objects are considered. The h function takes as input all the $y = g()$ generated from object being in relation with the current object processed, i.e for $v_2$ we use $g_o$ and $g_s$ because $v_2$ is in relation with $v_1$ and $v_3$.

Then, the new graph is processed to go from graph to image:

![graph to image](https://github.com/D3lt4lph4/papers/blob/master/docs/images/scenegraph/imagegenerationfromscenegraph/graph_to_graph.png?raw=true "Graph To Image")

This steps is used for each objects and works in two pipelines, the bottom one generates the bounding box, the top one the mask inside the box. Then all the output are merged together and presented to a [Cascade Refinement Network](https://arxiv.org/abs/1707.09405) to generate the final image.

Finally for the training they use a pair of discriminator networks and train in a adversarial fashion.
