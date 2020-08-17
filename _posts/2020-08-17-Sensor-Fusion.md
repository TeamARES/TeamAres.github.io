---
layout: post-no-feature
title: "Sensor Fusion and Localization"
desciption: "Introduction to Sensor Fusion using Kalman Filters!"
Owner: "Harsh Gupta"
about: "Harsh is the software lead at Team ARES. He has a knack for competitive programming, machine and deep learning and robotics."
linkdin: "https://www.linkedin.com/in/harsh-gupta-202418187/"
ownimage: "harsh-profile.jpeg"
category: articles
tags: [introm beginner, Sensor fusion, Localization, Kalman Filters]
date: 2020-08-17
image:
	feature: "https://blog.lidarnews.com/wp-content/uploads/2018/02/scale.gif"
---

## Preface:

- Have you ever wondered how do robots and self-driving cars navigate in their environment without any human intervention? They are not only able to navigate their way through but are also able to interact with the environment in many ways. But how can they do so if they are not fully aware about their position in the world and in their local enviroment? 
- Just imagine being asked to escape a room full of traps and obstacles having no vision and whereabouts of your current position. Well, just as we humans have our sense organs to help us better perceive the environment, similarly the robot or self-driving cars have a lot of sensors which help them to navigate and interact with the environment around them. These sensors include Inertial Measurement Units (IMU), Wheel Encoders, Stereo Cameras, Depth Cameras, GPS,etc.

## But Wait, Why Sensor "Fusion"?

- Okay, so by now we understand the importance of having a lot of sensors onboard to safely move around in the environment. But then what do we mean by sensor "fusion"? I mean we do have all our sensors giving us the information we want, so isn't our work done? As it turns out, it is not! 

### Problem with Sensors:

- All the sensors we use are not absolutely correct. Moreover, certain information that is extracted from these sensors is subject to discrete jumps and the error associated with them grows over time. For example: When we extract the information about the distance travelled over time by using the data from the IMU, due to the double integration term involved in the calculation, the error accumulates and grows exponentially with time.

- In addition to this, there are various types of unavoidable disturbances which also get accumulated with time as our robot moves around.

### The Next Step:

- So, how do we resolve this issue? This is where a very powerful technique known as sensor fusion comes into action. The basic idea is to take data from different sensors present in our system and then "fuse" them together to provide a much more accurate estimation of the variables involved. How exactly we "fuse" this data will be explained in the upcoming section.

## Kalman Filters:

- One of the most iconic use of Kalman Filters was to send and bring back the crew to the moon during the Apollo 11 mission. 

- A Kalman filter can be used for data fusion to estimate the state of a dynamic system (evolving with time) in the present (filtering), the past (smoothing) or the future (prediction).* 

* So, we at team ARES use the Extended Kalman Filter(which is the extension of the Kalman Filter) to fuse the data coming from the GPS, the IMU and the wheel encoders with the visual odometry data derived from the depth camera to get an accurate estimate of out current location, velocity and orientation in the local and global map.

* Since in the real world applications, Extended Kalman are much more useful as compared to the Kalman Filters, hence we will dive deeper into the theory and the mathematical formulations linked with EKF. 

## Extended Kalman Filter:

### Limitations of the Kalman Filter:

* Always work with Gaussian Distribution.

* Always work with linear functions.

* In most real world applications, the functions that we deal with are non-linear and hence Kalman filters fails to give us an accurate estimate.

### Moving towards EKF:

- We convert the non-linear functions into linear ones by approximation. We take help of a powerful tool called the Taylor Series which helps to get us a linear approximation of a non-linear function. 

- We are only interested in the first derivative of the Taylor Series. We draw a tangent around the mean and try to approximate the function linearly. 

  #### Linearizing a Non-Linear function using Taylor Series

![Linearizing a Non-Linear function using Taylor Series](https://miro.medium.com/max/634/1*bnzyD6t3pviEMlEndErMEg.jpeg)



## Mathematical Formulation:

#### 1) Prediction:

- Predicted state estimate

  ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/bb90d364383982306ba9eff791e69e512ab13603)

- Predicted Covariance estimate

  ​									![](https://wikimedia.org/api/rest_v1/media/math/render/svg/f9661a6d4993e4d0ef05d8191d2165749c767dc9)

#### 2) Update:

- Innovation or measurement residual

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/5ccbaa00f4e79b8d412fe82451cdde024fe71312)

- Innovation (or residual) covariance

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/4c76fff15959980bfe6252d433e8afefb09cd2ef)

- Near-optimal* Kalman gain

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/e18a0e284e91cbe44dfc9d079db4cb0964c308b7)

- Updated state estimate

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/553617ff1809cab332edbc112e2ab40a319f4415)

- Updated covariance estimate

  ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/e6a2ac5ac0b73066b922fa9e8ada695935d0f45d)

where the state transition and observation matrices are defined to be the following Jacobians

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/0066adf747f84efb3a6ee9e167bc45ebfc09ad5d)

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/bd13cc1b023148bc139982ef40209af87cfede75)

- We will not dive deeper into the mathematical part because this blog mainly focuses on the ideology and intuition behind fusing sensors. 

####    Block Diagram showing the process of sensor fusion using EKF

![Extended Kalman Filter Block-Diagram](https://www.researchgate.net/profile/Shijoh_V/publication/259885787/figure/fig2/AS:643946569023515@1530540234750/Block-diagram-of-state-estimator-The-n-dimensional-state-variable-x-with-mean-k-1-x.png)

## Summary:

- I hope that this blog gave you a basic idea of what sensor fusion is and why do we need it, what are the various problems associated with sensors and how can we overcome them using algorithms like Kalman Filters.
- The use of Kalman Filters is not only limited to sensor fusion and self-driving cars and robots. They are now being used to carry out many control activities. They also give us a much better result as compared to the traditional Backtracking algorithm for training Neural Networks.
- The implementation of sensor fusion using ROS packages will be covered in the next part of this blog. We would also simulate our very own robot and see sensor fusion in practise. Until then, you can check out our implementation of sensor fusion using robot_localization package in our [github](https://github.com/TeamARES/Sensor-Fusion) repository. 

## Links:

* [A great blog to read more about EKF](https://towardsdatascience.com/extended-kalman-filter-43e52b16757d)

* [Visual representation of Sensor Fusion using Kalman Filters](https://www.bzarg.com/p/how-a-kalman-filter-works-in-pictures/)

