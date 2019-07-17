# ImageNet-trained CNNs are biased towards texture; increasing shape bias improves accuracy and robustness

_last modified : 17-07-2019_

## General Information

- Title: ImageNet-trained CNNs are biased towards texture; increasing shape bias improves accuracy and robustness
- Authors: Robert Geirhos, Patricia Rubisch, Claudio Michaelis, Matthias Bethge, Felix A. Wichmann, Wieland Brendel
- Link: [article](https://arxiv.org/abs/1811.12231)
- Date of first submission: 29 Nov 2018
- Implementations:

## Brief

It is commonly thought in the machine learning community that CNN classifiers learn to classify the shapes of the objects. More specifically, they learn simple pattern in the first layers of the networks that are then combined to created more complex features which are then used to do the classification.

The authors of this article argue that the classification networks learn the textures rather than the shapes of the objects. They first show by simple experiments that the networks actually tend to use texture over shapes and then propose a solution.

## How Does It Work

Many experiments are carried to prove that classification neural networks use the texture to differentiate between images. The main experiment to provethey have a bias towards texture is the cue experiment. The texture of the images were changed and neural networks were to classify the results. The figure below shows that for most of the classes used, the neural networks have a bias towards texture. For comparison, they carry the same experiment on humans and the opposite happens, they mostly classify on shapes.

![textures vs shapes](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/knowingyournetwork/TextureLearning/texture_shapes.png "textures vs shapes")

**Caption from the article**: "Classification results for human observers (red circles) and ImageNet-trained networks AlexNet (purple diamonds), VGG-16 (blue triangles), GoogLeNet (turquoise circles) and ResNet-50 (grey squares). Shape vs. texture biases for stimuli with cue conflict (sorted by human shape bias). Within the responses that corresponded to either the correct texture or correct shape category, the fractions of texture and shape decisions are depicted in the main plot (averages visualised by vertical lines). On the right side, small barplots display the proportion of correct decisions (either texture or shape correctly recognised) as a fraction of all trials."

The solution proposed to prevent the networks for learning the texture over the shape is actually quite simple, they use style transfer on ImageNet (IN) in order to create a new dataset Stylized-ImageNet (SIN) that has the classes decorrelated from the textures. They trained networks on this dataset and tested them against some newly textured objects to see if they correctly classify the image.

## Results

The table below shows the different results for each of the possible mix of the training sets (IN/SIN). Here only the improvements on the original ImageNet are shown as well as PASCAL VOC and COCO, see the article for more experiments.

| name | training | fine-tuning | top-1 IN | top-1 IN | PASCAL VOC mAP50 | COCO mAP50 |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| vanilla ResNet | N | - | 76.13 | 92.86 | 70.7 | 52.3 |
| | SIN | - | 60.18 | 82.62 | 70.6 | 51.9 |
| | SIN+IN | - | 74.59 | 92.14 | 74.0 | 53.8 |
| Shape-ResNet | SIN+IN | IN | 76.72 | 93.28 | 75.1 | 55.2 |

## In Depth

Checkout the paper.
