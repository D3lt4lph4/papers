# LIME

## General Information (main fields described, non-exhaustive list)

- Title: Why Should I Trust You ? Explaining the Predictions of Any Classifier
- Authors: Marco Tulio Ribeiro, Sameer Singh, Carlos Guestrin
- Link: [article](https://arxiv.org/abs/1602.04938)
- Date of first submission: 16 Feb 2016
- Implementations: (can be used for other framework)
  - [python](https://github.com/marcotcr/lime/tree/master/lime)
  - [R](https://github.com/thomasp85/lime)

## Brief

When training any machine learning algorithm for classification, it is hard if not impossible to know if the trained classifier uses the good features to make the classifications. This articles present a method to get some insight as to why the classifier made a choice. For now, the main measure used to assess the quality of a model is the loss function, but there are some cases where the loss function can get low but use the "wrong" features for someone to generalize on other dataset (over-fitting).

The image below shows what one can expect from LIME:

![Husky](https://github.com/D3lt4lph4/papers/blob/master/docs/images/knowingyournetwork/LIME/husky.png?raw=true "Husky explanation")

For instance here we can see that the classifier is wrong probably because of some bias in the training set, it uses snow to classify the image of the husky, which is not the kind of feature we would like to use for the classification.

## How Does It Work

The algorithm will consider the model to be a black box and will look for the data in the input that, if changed will change the result of the classification. The algorithm follows this workflow:

- vectorize the input in some features that a human will understand.
- hide some part of the vectorized input and look for the change in the output
- create a linear model to separate and show which part of the vector is used for the classification

To explain a bit more the 3 parts:

The vectorization of the input is to cut the whole input into smaller pieces. For instance, a text in word or group of words, an image in superpixels (groups of pixels).

Then the second part will hide part of the input (one of the word or of the super pixel) and look at the changes in the output. The main idea here is to say, "if I hide this part and the classification changes, then it must be used to make the classification"

Finally some linear explanation is made to explain the classification (see image below)

![Husky](https://github.com/D3lt4lph4/papers/blob/master/docs/images/knowingyournetwork/LIME/separation.png?raw=true "Husky explanation")

As explained in the paper: "The black-box model’s complex decision function f (unknown to LIME) is represented by the blue/pink background, which cannot be approximated well by a linear model.  The bold red cross is the instance being explained. LIME samples instances, gets pre-dictions using f, and weighs them by the proximity to the  instance  being  explained  (represented  here by size).  The dashed line is the learned explanation that is locally (but not globally) faithful.

## In Depth

(Work in progress)