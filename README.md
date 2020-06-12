# Behavioral Cloning for Self-Driving Cars
A supervised regression problem between the car steering angles and the road images in front of a car.

The project is based on the research by Nvidia.The network is a CNN which maps raw pixel inputs along with steering data from a log file and clones the behaviour of the steering in autonomous mode.

**Goals**

The goals / steps of this project are the following:

Use the simulator to collect data of good driving behavior.
Build, a convolution neural network in Pytorch that predicts steering angles from images.
Train and validate the model with a training and validation set.
Test that the model successfully drives around the track without leaving the road.

**Project Contents**
The project includes the following files:

self_driving_car.py containing the script to create and train the model.</br>

src_code.ipynb containing the notebook code to create and train the model.</br>

model.py as a helper function for loading the required model in drive.py.</br>

drive.py for driving the car in autonomous mode.</br>

model.h5 containing a trained convolution neural network.</br>

**Collecting Training Data**

The simulator can be run in two modes: training mode and autonomous mode.

In training mode, the user controls the movement of the car using the steering angle, throttle, and brakes. You can control the car using the keyboard or the mouse. During training mode, you can hit the record key and the simulator will start saving the driving data to a specific location. The driving data consists of each image from the left, right, and front cameras (160x320x3 dimensions) of the car as well as the corresponding steering, throttle, and brake measurements.


To collect the training data, the car was driven in training mode around the track for two full laps using center lane driving behaviour. The data was then further reinforced with selective driving behaviour around corners to account for over-steer and under-steer, this allowed the model to learn the larger steering angle required to go around these corners.

The following is a diagram of the NVIDIA neural network architecture taken from their blog:
![nvidia_neural_network](https://user-images.githubusercontent.com/10712535/84471091-a5f7d600-ac52-11ea-9760-d94653229134.png)


The NVIDIA neural network above consists of 9 layers: 1 normalization layer, 5 convolutional layers, and 3 fully connected layers.

My implementation of the CNN :

**Model summary:**
 (module): CarSimpleModel (</br>
    (conv_layers): Sequential (</br>
      (0): Conv2d(3, 24, kernel_size=(3, 3), stride=(2, 2), bias=False)</br>
      (1): ELU (alpha=1.0)</br>
      (2): Conv2d(24, 48, kernel_size=(3, 3), stride=(2, 2), bias=False)</br>
      (3): MaxPool2d (size=(4, 4), stride=(4, 4), dilation=(1, 1))</br>
      (4): Dropout (p = 0.25)</br>
    )</br>
    (linear_layers): Sequential (</br>
      (0): Linear (3648 -> 50)</br>
      (1): ELU (alpha=1.0)</br>
      (2): Linear (50 -> 10)</br>
      (3): Linear (10 -> 1)</br>
    )</br>
 
I've added an additional dropout layer to avoid overfitting after the convolution layers.</br>

**Pytorch and CUDA**
Pytorch provides an easy integration with CUDA enabled GPUs. This is done with a simple device() function. It can immensely speed up the training process, like 10x faster than a normal CPU. For that, we need to transfer our data and the model to GPU for processing. 

**Challenges:**</br>
I think the most challenge is generating enough data for your model. For some tricky curves on the road, you need to create more data.</br>
Building a model in Pytorch is not as straightforward as in Keras. You need to understand the framework and how it processes data first.</br>
Need to create a Dataloader for your own data.</br>
Re-use as much code as possible.</br>
You might see the car wobble a lot or maybe it is confined to one side of the road. This might mean that the data is not augmented and generalized properly. Try to acquire more training data or augment with more randomness.</br>


