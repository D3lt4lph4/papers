# How transferable are features in deep neural networks?

_last modified : 30-06-2020_

## General Information

- Title: How transferable are features in deep neural networks?
- Authors: Jason Yosinski, Jeff Clune, Yoshua Bengio and Hod Lipson
- Link: [article](https://arxiv.org/abs/1411.1792)
- Date of first submission: 6 Nov 2014
- Implementations: (if any found)
  - [Keras](http://awesomelink1)
  - [Caffe](http://awesomelink2)

## Brief

**Problem:** Neural networks seem to work in two parts, the first part extracts general features and the second solve the target task. Wether the transition for the first to second part is smoothed over the whole network or is sharp between two layers has not been studied yet.

**Solution:** In this paper the authors propose to study such transition. More specifically, they experimentally quantify the concept of generality vs specificity. Generality being the fact that a given layer could be used for various tasks and specificity the fact that a layer can only serve to a peculiar task.

**Evaluated on:** The evaluate on ImageNet.

**Results:** They show that the transition seems to be quite sharp between generality and specificity. They also show that pre-training on an other unrelated dataset may help improving the accuracy of a network.

## How Does It Work

To test the generality and specificity of the layers of a network, they train two networks on two separate subset (A and B) of ImageNet (roughly divided in half) and then use part of the layers trained on the subset A to re-train on the subset B. They test in two different approches for retraining on the B subset: freezing the transfered weights and fine-tuning only the last weights or fine-tuning all the weights. The whole system is shown in the image below:

![system]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/others/howtransferablefeaturedeepnn/system.png "system")

B3B in this example means that the network was trained once on the subset B and then the first three layers where used to initialized an other network that is trained on the same subset B (A3B is trained on A, retrained on B). The + sign denotes the freezing or unfreezing of the weights.

## Results

Results are shown in the figures below:

![results]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/others/howtransferablefeaturedeepnn/results.png "results")

Details:

- baseB: Original network trained on B
- selffer BnB: Network retrained using the n first layers of B (frozen) on B
- selffer BnB+: Network retrained using the n first layers of B (unfrozen) on B
- transfer AnB: Network retrained using the n first layers of A (frozen) on B
- transfer AnB+: Network retrained using the n first layers of A (unfrozen) on B

We can see that the more frozen layers from A are used, the worse the accuracy on B. This seems to indicate that the generality to specificity transition point for this network is somewhere around layers 3/4. What is more interesting is the boost in accuracy when using unfrozen layers from A which always outperform the other methods.
