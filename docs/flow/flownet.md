# FlowNet: Learning Optical Flow with Convolutional Networks

_last modified : 11-02-2020_

## General Information

- Title: FlowNet: Learning Optical Flow with Convolutional Networks
- Authors: Philipp Fischer, Alexey Dosovitskiy, Eddy Ilg, Philip Häusser, Caner Hazırbaş, Vladimir Golkov, Patrick van der Smagt, Daniel Cremers, Thomas Brox
- Link: [article](https://arxiv.org/abs/1504.06852)
- Date of first submission: 26 Apr 2015
- Implementations: 
    - [PyTorch](https://github.com/ClementPinard/FlowNetPytorch)

## Brief

This paper introduce the usage of CNNs for the prediction of Optical Flow. They compare two architectures and introduce a new dataset to help training neural networks.

They train two architectures, one with standard CNN, the other with explicit convolutions.

They acheive state of the art results for real time methods.

## How Does It Work

### Networks

They present two network in the article, a straight forward version and a more complexe one. The straight forward version is made of stacked convolution followed by upconvolutions (following classical FCN). The second version adds an explicit convolution to the network to help it learn the displacement of the objects. The range of the add convolution is limited to limit the calculations. In both of the networks they have skip connections with the upper layers to input more information.

Both of the networks are shown in the following picture:

![network](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/FlowNet/network.png "network")

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