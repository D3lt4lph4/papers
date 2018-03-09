# Online Multi-Target Tracking Using Recurrent Neural Networks

## General Information

- Title: Online Multi-Target Tracking Using Recurrent Neural Networks
- Authors: Anton Milan, S. Hamid Rezatofighi, Anthony Dick, Ian Reid and Konrad Schindler
- Link: [article](https://arxiv.org/abs/1604.03635)
- Date of first submission: 13 Apr 2016
- Implementations:
    - [Torch/Lua](https://bitbucket.org/amilan/rnntracking)


## Brief

This is a fast online multi-target tracking network. The main idea is to make use of a LSTM and a RNN to predict the position as well as the state of the tracked object(s). 

The main advantage of this method compared to the others existing ones (at the time of the article) is the speed. According to the results presented, this method can run at 165 FPS when the others top at 32 starting at 1 FPS.

The second advantage of this method is that it does not look at all in the future to make the predictions, making it completely real time.

But on the other hand, it is a bit less performing than the other algorithms and the implementation is for tracking one object at a time (what's with the name ?) even if it could be changed to support multiple objects at once (diy). 

Also they do not perform the detection !


## How Does It Work

The network is separated into two main blocks, one for the predictions and one for the assignment of the predicted results.

Exactly, the first block predicts:
  - The predicted states for all target
  - The predicted updated states
  - The Birth/Death of the object
  - The absolute difference between current and previous Birth/Death state

And the second:
  - The association between the prediction and detected objects

So the first block tells you were your object will be and the second, with which detected object you should pair it.

## In Depth

The architecture of the network is described in the following image :

![How Does It Work](https://github.com/D3lt4lph4/papers/blob/master/docs/images/tracking/onlinemultitrackingRNN/network.png?raw=true "Network architecture")

The second part, the less complicated one is a LSTM with some weights added at the end. 
The C variable is the norm between the prediction and the detected objects and is used to associate the prediction with an object.

The first part, the most complex one, is made up of three blocks:
  - The first one for the predictions
  - The second one outputs the predictions corrected with the help of the detections and birth/death vector, and the birth/death status
  - The last one gives the absolute difference between the new and previous birth/death state
 
 To explain a bit the variables:
  - The birth/death (E) basically tells if the object should (not) be tracked (is it still alive on screen)
  - The z is a vector contains the current detected objects and is used to correct the prediction with the current objects detected on screen
  - The A is here to tell, for each vector of z if it is to be associated with the prediction.
 
 
The important thing to notice here, is the loop made between the first and second part. The C in the LSTM requires the x output by the RNN which requires the output of the LSTM as input. It seems that the only way to overcome this results is to use the three separated blocks in the RNN part to first output the x*, use it to calculate the C, output the A and then use it to output the x in the update part (unless I'm missing something).
 
In the end the workflow is the following: Prediction => Association => Update/Death/Birth.
 