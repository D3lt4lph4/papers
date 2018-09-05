# Neural Motifs: Scene Graph Parsing with Global Context

_last modified : 05-09-2018_

## General Information

- Title: Neural Motifs: Scene Graph Parsing with Global Context
- Authors: Rowan Zellers, Mark Yatskar, Sam Thomson, Yejin Choi, Paul G. Allen
- Link: [article](https://arxiv.org/abs/1711.06640)
- Date of first submission: 17 november 2017
- Implementations:
    - [Pytorch](https://github.com/rowanz/neural-motifs)

## Brief

This article builds a network that uses both local and global structure. Their architecture is justified by a statistical analysis of the graphs used.

They show that some objects in the dataset are strongly linked to some other and that if you have the two objects there is a high probability to get some relation between the objects.

## How Does It Work

Their structure is made of following lstm layers to take advantage of the global structure of the graph while at the same time still having the local information.

The following figure shows the pipeline for creating a graph from an image:

![network pipeline](https://github.com/D3lt4lph4/papers/blob/master/docs/images/scenegraph/neuralmotifparsingwithglobalcontext/pipeline.png?raw=true "Network Pipeline")

The relation between the dog and the eye is kept thanks to the lstm.

## Results

Here put the results of the network, scores in competitions, ...

## In Depth

Here, go full description, tricks and all, keep in m