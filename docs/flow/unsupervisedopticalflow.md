# Unsupervised Deep Learning for Optical Flow

_last modified : 30-06-2020_

## General Information

- Title: Unsupervised Deep Learning for Optical Flow Estimation
- Authors: Zhe Ren, Junchi Yan, Bingbing Ni, Bin Liu, Xiaokang Yang, Hongyuan Zha
- Link: [article](https://www.semanticscholar.org/paper/Unsupervised-Deep-Learning-for-Optical-Flow-Ren-Yan/47bc34ae6f5dc104bc289ae3bb4fa75ef75fbc21)
- Date of first submission: 2017
- Implementations:

## Brief

**Problem:** It has been proven that Optical Flow estimation can be done using supervised learning techniques. However, the shortage of labeled datasets has forced the scientists to use generated dataset. Learning methods without labeled data is a task that is yet to be solved.

**Solution:** The authors propose to use unsupervised learning to avoid the need for synthetic datasets. Given two frames, they use the first to predict the second. The estimation of the optical flow is learnt as a subtask of their pipeline.

**Evaluated on:** They evaluate there methods on Flying Chair, Kitti and Sintel datasets.

**Results:** They do not manage to reach the state of the art results although they claim to come very close to it. The main interest of the method lies in the fact that the method is unsupervised, hence reducing the overall training costs by removing the need for annotations to get a working system.

## How Does It Work

The optical flow is the pixel displacement information between two images. As the optical flow is hidden yet present in two following frames, it is possible to train a network to estimate it without the actual label. By using the first frame to predict the second, the optical flow can be integrated as a part of the learning pipeline. The presented method for learning the optical flow (shown in the image below) is as follow:

- Predict the optical flow (Localization layer)
- Use the predicted optical flow to wrap the first frame
- Set a loss to compare the wrapped and original second frame and learn the overall network through backpropagation.

![image]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/unsupervisedopticalflow/network.png "image")

## Results

They get impressive results given the fact that they train in an unsupervised manner. The results table is not reproduced here as pure EndPoint Error as it is quite big and not so informative in the sense that it doesn't explicitly gives information about the visual quality of the methods. Rather, the images below gives a visual understanding of the quality of the predictions (DSTFlow is the method of this paper).

Flying Chairs:

![image1]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/unsupervisedopticalflow/chairs.png "image1")

Sintel:

![image2]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/unsupervisedopticalflow/sintel.png "image2")

Kitti:

![image3]( https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/flow/unsupervisedopticalflow/kitti.png "image3")
