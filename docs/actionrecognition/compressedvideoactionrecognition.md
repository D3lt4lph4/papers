# Compressed Video Action Recognition (in progress)

_last modified : 01-07-2020_

## General Information (main fields described, non-exhaustive list)

- Title: Compressed Video Action Recognition
- Authors: Chao-Yuan Wu, Manzil Zaheer, Hexiang Hu, R. Manmatha, Alexander J. Smola, Philipp Krähenbühl
- Link: [article](https://arxiv.org/abs/1712.00636)
- Date of first submission: 2 Dec 2017
- Implementations:
    - [PyTorch](https://github.com/chaoyuaw/pytorch-coviar)

## Brief

**Problem:** Processing video with deep neural networks as yield mitigated results when compared with handcrafted techniques. The authors argue that this is due to two main problems: redundancy in video images and difficulty to learn the temporal structure solely with RGB frames.

**Solution:** They propose a method that takes advantage of the compressed representation of the videos to carry action recognition. By using motion and residual information contained in the compressed video, they can provide the network with valuable new information and remove redundancy.

**Evaluated on:** They evaluate their method on three datasets, UCF-101, HMDB-51 and Charades.

**Results:** They claim that their approach outperforms all the other methods on the tested dataset while improving processing speed by using the compressed representation of the data.

## How Does It Work

The proposed solution relies heavily on motion vectors and residuals. When a video is compressed in mp4, it is decomposed in I-frames and P-frames. I-frames are frames encoded as a whole, and P-frames are frames partially encoded that relies on previous frames. The aim of a P-frame is to remove redundant information with the reference frame. In order to remove the redundancy, a P-frame is divided in blocks. Each of the blocks is match to the most resembling block in the reference frame. The displacement of the blocks gives us the motion vectors. As the blocks are matched with the "most resembling", motion vectors are not sufficient to encode the whole frame information, one needs to encode the difference between each of the matched blocks, this is the residual information.

They propose to rely on this motion and residual information to carry the action recognition task. They fusion the information from the I-frame and P-frame. The idea of the method is shown in the image below (in practice to extract the features,they use a ResNet-152 for I-frames and ResNet-18 for P-frames):

![image](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/actionrecognition/compressedvideoactionrecognition/method.png "image")

As the motion vectors and residuals tend to be noisy, they propose to "filter" this noise by using an accumulated version instead. The idea is that noise motion won't propagate well in time and won't have an intensity as strong as continuous motion as they do not represent long time dependencies. This is shown in the image below:

![image](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/actionrecognition/compressedvideoactionrecognition/motion_acc.png "image")

## Results

Their results can somewhat be summurized in the figure below:

![image](https://raw.githubusercontent.com/D3lt4lph4/papers/master/docs/images/actionrecognition/compressedvideoactionrecognition/results.png "image")
