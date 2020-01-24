# Accurate, Large Minibatch SGD:Training ImageNet in 1 Hour

(will be updated by a git hook on commit)
_last modified : 11-07-2019_

## General Information

- Title: Accurate, Large Minibatch SGD:Training ImageNet in 1 Hour
- Authors: Priya Goyal, Piotr Dollár, Ross Girshick, Pieter Noordhuis, Lukasz Wesolowski, Aapo Kyrola, Andrew Tulloch, Yangqing Jia, Kaiming He
- Link: [article](https://arxiv.org/abs/1706.02677)
- Date of first submission: 8 Jun 2017 
- Implementations:
    - [Horovod](https://github.com/horovod/horovod/blob/master/examples/keras_imagenet_resnet50.py)

## Brief

This article presents general guidelines to train a network in a distributed framework. They empirically show that the learning rate should be scaled linearly with the augmentation of the minibatch size. They introduce various notions for training in a distributed manner. They also raise some flags for the common pitfalls one could encounter when using the presented method. These two points are detailed in the next section.

When training a ResNet on ImageNet, they show that for minibatch size up to 8k (effectively training the network in 1h), there is almost no loss in the training accuracy.



## How Does It Work

Basically, when training a neural network, one can follow the following **Linear Scaling Rule**: When the minibatch size is multiplied byk, multiply the learning rate byk.

They introduce the notion of **Warmup** to help mitigate the instability of the training during the first epochs. During the 5 first epochs the learning rate is scaled up from the original one to the linearly scaled one.

They also discuss on the impact of the size of the batch on BatchNormalization (although they do not provide with insight for the selection of the batch size parameter)

Finally, they provide with guidelines for the subtleties and pitfalls of distributed SGD:

- Weight Decay
- Momentum correction
- Gradient aggregation
- Data shuffling

The guidelines are specific for each of the examples and not provided here, please refer to the article for more details (this is a quick memo on topics of interest).

## Results

The image below shows the validation error vs the mini-batch size. We can see that up to 8k images in a batch, there is almost no loss in the accuracy of the network. As stated in the conclusion, using this size of mini-batch is interesting if you do not care so much about accuracy.

![resultsSSSSSSS](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/others/AccurateLargeMinibatchSGD/results_figure.png "results")

Finally the table below gives 
