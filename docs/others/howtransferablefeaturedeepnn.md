# How transferable are features in deep neural networks?

_last modified : 30-03-2020_

## General Information

- Title: How transferable are features in deep neural networks?
- Authors: Jason Yosinski, Jeff Clune, Yoshua Bengio and Hod Lipson
- Link: [article](https://arxiv.org/abs/1411.1792)
- Date of first submission: 6 Nov 2014
- Implementations: (if any found)
    - [Keras](http://awesomelink1)
    - [Caffe](http://awesomelink2)

## Brief

Neural networks seem to work in two parts, the first part extracts general features and the second solve the target task. Wether the transition for the first to second part is smoothed over the whole network or is sharp between two layers has not been studied yet. In this paper the authors propose to study such transition. More specifically, they experimentally quantify the concept of generality vs specificity. Layers that could serve as feature extractor for various task are general while layers that can only serve to a peculiar task are specific.

Probably the most interesting result from the paper is that using a pre-trained network for initialization rather than random weights seems to lead to better generalization.

## How Does It Work

To test the generality and specificity of the layers of a network, they train two network on two separate subset of ImageNet (roughly half each) and then use part of the layers trained from the subset A to train on the subset B (and reversly). They test in two different manners, freeze the transfered weights and fine-tuning all the weights. The whole system is shown in the image below:

![system]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/others/howtransferablefeaturedeepnn/system.png "system")

## Results

Results are shown in the Figures below:

![results]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/others/howtransferablefeaturedeepnn/results.png "results")

Details:
- baseB: Original network trained on B
- selffer BnB: Network retrained using the n first layers of B (frozen) on B
- selffer BnB+: Network retrained using the n first layers of B (unfrozen) on B
- transfer AnB: Network retrained using the n first layers of A (frozen) on B
- transfer AnB+: Network retrained using the n first layers of A (unfrozen) on B


We can see that the more frozen layers from A is used, the worse the accuracy on B. This seems to indicate that the generality to specificity transition point for this network is somewhere around layers 3/4. What is more interesting is the boost in accuracy when using unfrozen layers from A which always outperform the other methods.
