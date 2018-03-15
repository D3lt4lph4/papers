# Recurrent Attention Model

## General Information

- Title: Recurrent Models of Visual Attention
- Authors: Volodymyr Mnih, Nicolas Heess, Alex Graves, Koray Kavukcuoglu
- Link: [article](https://arxiv.org/abs/1406.6247)
- Date of first submission: 24 Jun 2014
- Implementations:
    - [PyTorch](https://github.com/kevinzakka/recurrent-visual-attention)
    - [Tensorflow](https://github.com/jlindsey15/RAM)

## Brief

This article describe a detection workflow that simulate the way the human eye works. Rather than looking at the whole image and doing the classification, the agent looks at glimpse of the image and move his eye around to classify what it sees. It was presented as some alternative to the existing classifiers which needed first the extraction of ROI to work.

## How Does It Work

The architecture of the system is made of two main parts:

- A glimpse senor which can only see a part of the image, the agent never sees the full image
- A glimpse network which output two things, where to look next and the classification at the current position

The glimpse network makes use of RNN structure, thus the classification takes into account the previous states and should improve over time.

![RAM Description](https://github.com/D3lt4lph4/papers/blob/master/docs/images/imageclassif/ram/ram-network.png?raw=true "RAM Framework")