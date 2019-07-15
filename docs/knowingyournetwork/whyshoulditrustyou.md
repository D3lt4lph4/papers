# LIME

_last modified : 15-07-2019_

## General Information (main fields described, non-exhaustive list)

- Title: Why Should I Trust You ? Explaining the Predictions of Any Classifier
- Authors: Marco Tulio Ribeiro, Sameer Singh, Carlos Guestrin
- Link: [article](https://arxiv.org/abs/1602.04938)
- Date of first submission: 16 Feb 2016
- Implementations: (can be used for other framework)
    - [python](https://github.com/marcotcr/lime/tree/master/lime)
    - [R](https://github.com/thomasp85/lime)

## Brief

Currently, when training any machine learning algorithm for classification, it is hard if not impossible to know if the trained classifier uses the "correct features" to make the classifications. Thus it makes it hard for the end user to trust the classifier and for the data scientist to find the features that may biased the network. This article presents a method to get some insight as to why a classifier made a choice.

So far, the main measure used to assess the quality of a model is the loss function, but there are some cases where the loss function can get low but use the "wrong" features, thus making the classifier unable to generalize to an other dataset (over-fitting). 

The image below is a perfect example of a model that could get an excellent loss on a validation test but poor results on real datasets.

![Husky](https://github.com/D3lt4lph4/papers/blob/master/docs/images/knowingyournetwork/LIME/husky.png?raw=true "Husky explanation")

The image shows the reason why the classifier classified this image  (a husky) as a wolf. As can be seen it uses the snow to make the classification. The reason for that is that during the training, all the wolf images had snow in it. The model was performing quite good on the validation dataset because of that, but cannot be used on a new dataset because the features used for the classification is wrong.

## How Does It Work

The classifier is considered as a black box, then the input is transformed into an understandable representation (super-pixels, bag of word, ...) and, locally an approximation is made with an "explainable model" (see In Depth).

![Linear Separation](https://github.com/D3lt4lph4/papers/blob/master/docs/images/knowingyournetwork/LIME/separation.png?raw=true "Husky explanation")

As explained in the paper: "The black-box model’s complex decision function f (unknown to LIME) is represented by the blue/pink background, which cannot be approximated well by a linear model.  The bold red cross is the instance being explained. LIME samples instances, gets pre-dictions using f, and weighs them by the proximity to the  instance  being  explained  (represented  here by size).  The dashed line is the learned explanation that is locally (but not globally) faithful."

## Results

Limitation on the speed of your classifier.

## In Depth

The article revolves around the idea of "explainable model". The explainable models are simpler model such as linear models.

Let's take the following example:

\[ y = 2 * x_1 + (-4) * x_2 + ... + c_l * x_l\]

If we consider the case where a positive y means class 1 and negative y means class 2, then all the positive coefficient are linked to features "helping" the first class and the negative ones are "helping" the second class (the x are 0 or 1 to tell if the feature is here or not).

Once you have that idea of "explainable model", the algorithm is straight forward, once again with an example:

- take an image, and cut it down in super-pixels
- hide randomly some of the super-pixels to create a set of "around the original" images
- this set is made of two inputs, the images (ims) with the super-pixels grayed and vectors of 0 and 1 (vs) to tell if the ith super-pixel in the image is grayed or not.
- feed the images (ims) of the set to the original classifier to get outputs.
- learn the explainable model using the vectors of 0 and 1 (vs) and the generated outputs
