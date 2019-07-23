# Image Generation from Scene Graph

_last modified : 01-09-2018_

## General Information

- Title: Image Generation from Scene Graph
- Authors: Justin Johnson, Agrim Gupta and Li Fei-Fei
- Link: [article](https://arxiv.org/abs/1804.01622)
- Date of first submission: 4 April 2018
- Implementations:
    - [Python](https://github.com/google/sg2im)

## Brief

Methods exist to generate image from natural language descriptions. These methods can take various forms, for instance, RNN coupled with GANs.  In this article, the authors propose to improve the results obtained on these methods by capturing more information about the image to generate using scene graphs. No insight is given as to how generate the scene graph as an input.

## How Does It Work

To solve the problem they propose an end to end network. The network has two main parts, the first one processes the graph to create the features representative of the description of the image. And the second part takes the features and uses them to create the image representing the scene.

This image from the articles shows the whole pipeline:

![network pipeline](https://github.com/D3lt4lph4/papers/blob/master/docs/images/scenegraph/imagegenerationfromscenegraph/pipeline.png?raw=true "Network Pipeline")

First the input scene graph is transformed while keeping the graph structure. Then boxes and shapes representing the objects of the scene are predicted. Finally, from the representation of the scene, the image is generated with convolutional layers.

## Results

To test the proposed approach, the authors use the mechanical turk. They propose their image as well as the image from the state of the art network and ask the question: "Which image match the caption better ?" (the images were generated using the same caption). They show that their images are preferred in 67.6\% of the presented pairs of images.

## In Depth

Let's describe a bit more each steps of the network.

First the features are generated using the input scene graph. The graph is a series of relation between object, noted as ($o_i$ ,r ,$o_j$), object i in relation r with object j. All the object are linked to an other one.

From this graph there is a "one to one" mapping using a graph convolutions as describe in the following image:

![graph to graph](https://github.com/D3lt4lph4/papers/blob/master/docs/images/scenegraph/imagegenerationfromscenegraph/graph_to_graph.png?raw=true "Graph to Graph")

For each vectors describing either a relation $v_r$ or an object $v_i$, new vectors are output. The function to output the new relation vectors differ from the function used to output the new object vectors because object may be linked to multiple object while relation are only between to objects.

Then, the new graph is processed to go from graph to image:

![graph to image](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/scenegraph/imagegenerationfromscenegraph/graph_to_image.png "Graph To Image")

This steps is used for each objects and works in two pipelines (inside the red rectangle), the bottom one generates the bounding box, the top one the masked embedding. The masked embedding is then interpolated inside the box in the description matrix. As said before, this step is done for all the objects (blue and green rectangles), and all the generated matrix are merged to get the scene layout.

Finally, the scene layout is presented to a [Cascade Refinement Network](https://arxiv.org/abs/1707.09405) to generate the final image. For the training they use a pair of discriminator networks and train in a adversarial fashion.
