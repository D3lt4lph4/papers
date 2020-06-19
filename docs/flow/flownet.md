# FlowNet: Learning Optical Flow with Convolutional Networks

_last modified : 19-06-2020_

## General Information

- Title: FlowNet: Learning Optical Flow with Convolutional Networks
- Authors: Philipp Fischer, Alexey Dosovitskiy, Eddy Ilg, Philip Häusser, Caner Hazırbaş, Vladimir Golkov, Patrick van der Smagt, Daniel Cremers, Thomas Brox
- Link: [article](https://arxiv.org/abs/1504.06852)
- Date of first submission: 26 Apr 2015
- Implementations: 
    - [PyTorch](https://github.com/ClementPinard/FlowNetPytorch)

## Brief

This paper introduce the usage of CNNs for the prediction of Optical Flow. They compare two architectures and introduce a new dataset (Flying Chairs dataset) to help training neural networks.

The main task is to predict the Optical Flow, or pixel displacement between two consecutive frames and to do so, they train two architectures: one with standard CNN and another using parallel branches and explicit correlation.

They achieve state of the art results for real time methods.

## How Does It Work

### Networks

The aim is to predict the optical flow between two images. To do so, they develop two architectures shown bellow:

![network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/FlowNet/network.png "network")

The top network is a classical FCN made of stacked convolution followed by upconvolutions. 

They also design a second network, the bottom one, based on a mix of CNN and correlation. The idea is to explicitly add a part designed to find the displacement between the two images. Skip connexions were also added to this architecture.

### Dataset: Flying Chairs

Because deep learning requires a lot of data to learn a model, they introduce a new dataset for optical flow estimation. This dataset is made of flying chairs moving on top of Flickr images. The chairs are moving following affine transformations.

With this dataset they manage to improve their results. They also added data-augmentation to get the most of their networks (all the data-augmentation parameters are given in the article).

## Results

They compare themselves with other methods on various datasets. They use the End Point Error for the evaluation. Not all the results are shown in the table, ft and v stand for fine-tuning and variational refinement (not detailed here).

| Method | Sintel Clean | Sintel Final | KITTI | Middlebury test AEE | Middlebury test AEE | Chairs | Time (sec) CPU | Time (sec) GPU|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| EpicFlow | 4.12 | 6.29 | 3.8 | 0.39 | 3.55 | 2.94 | 16 | - |
| DeepFlow | 5.38 | 7.21 | 5.8 | 0.42 | 4.22 | 3.53 | 17 | - |
| EPPM  | 6.49 | 8.38 | 9.2 | 0.33 | 3.36 | - | - | 0.2 |
| LDOF  | 7.56 | 9.12 | 12.4 | 70.56 | 4.55 | 3.47 | 65 | 2.5 |
| FlowNetS  | 7.42 | 8.43 | - | - | - | 2.71 | - | 0.08 |
| FlowNetS+v | 6.45 | 7.67 | - | - | - | 2.86 | - | 1.05 |
| FlowNetS+ft | 6.96 | 7.76 | 9.1 | - | - | 3.04 | - | 0.08 |
| FlowNetS+ft+v | 6.16 | 7.22 | 7.6 | 0.47 | 4.58 | 3.03 | - | 1.05 |
| FlowNetC | 7.28 | 8.81 | - | - | - | 2.19 | - | 0.15 |
| FlowNetC+v | 6.27 | 8.01 | - | - | - | 2.61 | - | 1.12 |
| FlowNetC+ft | 6.85 | 8.51 | - | - | - | 2.27 | - | 0.15 |
| FlowNetC+ft+v | 6.08 | 7.88 | - | 0.50 | 4.52 | 2.67 | - | 1.12 |