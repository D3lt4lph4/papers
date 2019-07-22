# Recurrent Attention Model

_last modified : 19-07-2019_

## General Information

- Title: Recurrent Models of Visual Attention
- Authors: Volodymyr Mnih, Nicolas Heess, Alex Graves, Koray Kavukcuoglu
- Link: [article](https://arxiv.org/abs/1406.6247)
- Date of first submission: 24 Jun 2014
- Implementations:
    - [PyTorch](https://github.com/kevinzakka/recurrent-visual-attention)
    - [Tensorflow](https://github.com/jlindsey15/RAM)

## Brief

The authors argue that applying convolutional neural networks to large image can be computationally expensive and thus aim to provide a new method to reduce this cost. The article describe a detection/classification workflow that simulate the way the human eye works. Rather than looking at the whole image and to do the classification, the agent looks at glimpse of the image and move his eye around to classify what it sees.

## How Does It Work

The solution proposed is an RNN. The RNN can see only part of the image and has to output the next location to look at. More exactly, the network is composed of four main functions (c.f figure below):

- glimpse network, $f_g(\theta_g)$, which outputs a representation of a glimpse
- core network, $f_h(\theta_h)$, to calculate an internal state given the new features and the previous states
- location network, $f_l(\theta_l)$, to output the new location given the current state
- action network, $f_a(\theta_a)$, to output the action (for instance classification) given the current state

![RAM Description](https://github.com/D3lt4lph4/papers/blob/master/docs/images/imageclassif/ram/ram-network.png?raw=true "RAM Framework")

The network has to be trained using reinforcement learning techniques. For instance, there is no ground truth for the best place to look at, the network has to guess for itself.

## Results

They test on different datasets and outperform the convolutional and fully connected layers. The tables below show some results, refer to the paper for more details. The number of glimpse is the number of time the network was allowed to look at the image.

| Model | Error |
|:--:|:--:|
| FC, 2 layers (256 hiddens each) | 1.69% |
| Convolutional, 2 layers | 1.21% |
| RAM, 2 glimpses,8x8 , 1 scale | 3.79% |
| RAM, 3 glimpses,8x8 , 1 scale | 1.51% |
| RAM, 4 glimpses,8x8 , 1 scale | 1.54% |
| RAM, 5 glimpses,8x8 , 1 scale | 1.34% |
| RAM, 6 glimpses,8x8 , 1 scale | 1.12% |
| RAM, 7 glimpses,8x8, 1 scale | 1.07% |

| Model | Error |
|:--:|:--:|
| FC, 2 layers (64 hiddens each) | 6.42% |
| FC, 2 layers (256 hiddens each) | 2.63% |
| Convolutional, 2 layers | 1.62% |
| RAM, 4 glimpses,12x12 , 3 scales | 1.54% |
| RAM, 6 glimpses,12x12, 3 scales | 1.22% |
| RAM, 8 glimpses,12x12, 3 scales | 1.2% |

## In Depth

Check the articles for more details.