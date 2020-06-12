# Behavioral Cloning for Self-Driving Cars
A supervised regression problem between the car steering angles and the road images in front of a car.

The project is based on the research by Nvidia.The network is a CNN which maps raw pixel inputs along with steering data from a log file and clones the behaviour of the steering in autonomous mode.

The project consisted of the following stages:

Collect training data by driving the car around the simulator.
Implement the NVIDIA neural network.
Train and test model performance.

**Collecting Training Data**

The simulator can be run in two modes: training mode and autonomous mode.

In training mode, the user controls the movement of the car using the steering angle, throttle, and brakes. You can control the car using the keyboard or the mouse. During training mode, you can hit the record key and the simulator will start saving the driving data to a specific location. The driving data consists of each image from the left, right, and front cameras (160x320x3 dimensions) of the car as well as the corresponding steering, throttle, and brake measurements.


To collect the training data, the car was driven in training mode around the track for two full laps using center lane driving behaviour. The data was then further reinforced with selective driving behaviour around corners to account for over-steer and under-steer, this allowed the model to learn the larger steering angle required to go around these corners.

The following is a diagram of the NVIDIA neural network architecture taken from their blog:
![nvidia_neural_network](https://user-images.githubusercontent.com/10712535/84471091-a5f7d600-ac52-11ea-9760-d94653229134.png)



