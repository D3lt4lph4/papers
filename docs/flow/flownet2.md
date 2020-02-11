# FlowNet 2.0: Evolution of Optical Flow Estimation with Deep Networks

_last modified : 11-02-2020_

## General Information

- Title: FlowNet 2.0: Evolution of Optical Flow Estimation with Deep Networks
- Authors: Eddy Ilg, Nikolaus Mayer, Tonmoy Saikia, Margret Keuper, Alexey Dosovitskiy, Thomas Brox
- Link: [article](https://arxiv.org/abs/1612.01925)
- Date of first submission: 6 Dec 2016
- Implementations: (if any found)
    - [Pytorch](https://github.com/NVIDIA/flownet2-pytorch)
    - [Caffe](https://github.com/lmb-freiburg/flownet2)

## Brief

In this paper, the authors focus on improving the optical flow estimation with deep learning. They work on the previously introduced FlowNet and improve the precision of the network through 3 main improvements:

- Data scheduling: They show that the order the data is presented to the network has an impact on the final precision
- Iterative learning: Copying other methods, they stack networks to carry some iterative refinement. To simplify the work of the added networks, they use a wrapping operation
- Small displacements improvements: Introduction of a new dataset and minor changes to the network

They also introduce small version of their networks to improve on the speed of prediction while maintaining the precision of FlowNet.

With the proposed improvements, they outperform the previous FlowNet network and reach precisions that matches the state of the art.

## How Does It Work

### Dataset scheduling

They show that for a given a learning rate schedule, it is better to first train on a simple dataset and then to finetune on the complicated one. It is still unclear to me how they choose the learning rate schedule and why they train and finetune on the same dataset for some of the experiments.

### Iterative learning

They stack networks in order to improve the results in an iterative manner. The first networks gets the two input images and the following ones gets the two images and the flow prediction from the previous network. They also wrap one of the images input to the added networks using the predicted flow to simplify the prediction work (see image below for more visual details).

### Displacement improvements

The FlowNet network seems to have trouble estimating small displacement. To understand why, they analyze the training data previously used and find that it contains mainly large displacement. They introduce a new dataset with small displacements to improve on this predictions.

They also carry some modification on their architecture to improve the results. The final network is shown below:

![network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/FlowNet2/network.png?raw=true "network")

## Results

The results are summarized in the following graph:

![results](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/FlowNet2/results.png?raw=true "results")

They show large speed/precision improvements and are on par with the state of the art methods.
