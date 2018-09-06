# Hierarchical Multi-Label Classification 

_last modified : _

## General Information

- Title: Hierarchical Multi-Label Classification
- Authors: Jônatas Wehrmann, Ricardo Cerri, Rodrigo C. Barros
- Link: [article](http://proceedings.mlr.press/v80/wehrmann18a/wehrmann18a.pdf)
- Date of first submission: February 2014
- Implementations:

## Brief

This approach tries to mix both local and global prediction used to generate hierarchical classification.

They propose two architecture for their network, one using feed-forward layers and the other inspired from lstm.

One of the main difficulties raised in the paper was the size of the datasets, small for many classes.

## How Does It Work

The feed-forward network works in multiple steps, predictions are made for each level of the hierarchical classification and at the end, using the classification at each level and the global one, the final predictions are output.

The recurrent network comes from the lack of scalability of the feed-forward network, the idea is the same as the one for the feed-forward network, but this time, a recurrent layer is re-used to compute the local predictions.

## Results

They tested their networks on 21 different datasets and compared the results with other approach.

The following table regroups all the results on the 21 datasets:

| DATASET | HMCN-F | HMCN-R | CLUS-HMC | CSSA | CLUS-ENS | HMC-LMLP |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| CELLCYCLE(FUNCAT) | 0.252 | 0.247 | 0.172 | 0.188 | 0.227 | 0.207 |
|DERISI(FUNCAT) | 0.193 | 0.189 | 0.175 | 0.186 | 0.188 | 0.183 |
|EISEN(FUNCAT) | 0.298 | 0.298 | 0.204 | 0.212 | 0.271 | 0.245 |
|EXPR(FUNCAT) | 0.301 | 0.300 | 0.210 | 0.220 | 0.271 | 0.243 |
|GASCH1 (FUNCAT)| 0.284 | 0.283 | 0.205 | 0.208 | 0.267 | 0.236 |
|GASCH2 (FUNCAT)| 0.254 | 0.249 | 0.195 | 0.210 | 0.227 | 0.211 |
|SEQ(FUNCAT) | 0.291 | 0.290 | 0.211 | 0.218 | 0.284 | 0.236 |
|SPO(FUNCAT) | 0.211 | 0.210 | 0.186 | 0.208 | 0.210 | 0.186 |
|CELLCYCLE(GO)| 0.400 | 0.395 | 0.357 | 0.366 | 0.387 | - |
|DERISI(GO)| 0.369 | 0.368 | 0.355 | 0.357 | 0.363 | - |
|EISEN(GO)| 0.440 | 0.435 | 0.380 | 0.401 | 0.433 | - |
|EXPR(GO)| 0.452 | 0.450 | 0.368 | 0.384 | 0.418 | - |
|GASCH1 (GO)| 0.428 | 0.416 | 0.371 | 0.383 | 0.415 | - |
|GASCH2 (GO) | 0.465 | 0.463 | 0.369 | 0.373 | 0.395 | - |
|SEQ(GO)| 0.447 | 0.443 | 0.386 | 0.387 | 0.435 | -|
|SPO(GO)| 0.376 | 0.375 | 0.345 | 0.352 | 0.372 | -|
|DIATOMS| 0.530 | 0.514 | 0.167 | - | 0.379 | -|
|ENRON| 0.724 | 0.710 | 0.638 | - | 0.681 | -|
|IMCLEF07A| 0.950 | 0.904 | 0.574 | - | 0.777 | -|
|IMCLEF07D| 0.920 | 0.897 | 0.749 | - | 0.863 | -|
|REUTERS | 0.649 | 0.610 | 0.562 | - | 0.703 | - |
|AVERAGERANKING| 1.07 | 2.04 | 5.12 | 3.96 | 3.57 | - |

## In Depth

### Feed-Forward

![Feed forward]

The architecture of the feed forward network is described below:
![feedforward](https://github.com/D3lt4lph4/papers/blob/master/docs/images/hierarchicalclassification/hierarchicalmultilabelclassificationsnetworks/ff_network.png?raw=true "Feed Forward")

x is the input and the P are the predictions, $P_G$ is the prediction at the global level and the $P_L$ are the predictions at the local level. The factor $\beta$ controls how much of the local and global are retained in the final prediction.

### Recurrent

The diagram below describes the lstm inspired architecture for the network:

![lstm](https://github.com/D3lt4lph4/papers/blob/master/docs/hierarchicalclassification/hierarchicalmultilabelclassificationsnetworks/lstm_network.png?raw=true "LSTM")

The same idea is applied, there are prediction at each level, but this time, the recurrent layer is used to predict the output. And at the end, global and local predictions are process with the same $\beta$ factor.