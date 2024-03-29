---
title: SLAM
author: Govind Saju
hero_image: "/ERC-website-2021/static/slam_cover.jpg"
date: 2021-11-24T12:30:00Z

---
The objective of SLAM is to estimate a robot’s state (position and orientation) and create a map of the robot’s surroundings simultaneously using the knowledge of its controls and the observations made by its sensors.

# Introduction

The term SLAM is an acronym for “Simultaneous Localization and Mapping”.

**Localization**: Localization refers to the robot's ability to estimate its own position and orientation with respect to its surroundings. This is done by combining the robot's controls along with the data obtained from its sensors.

**Mapping**: Creating a map of the robot’s surroundings using its estimate on its position and the data obtained from various sensors.

SLAM aims to do both of these tasks simultaneously, using one to help improve its estimate of the other. This may not sound possible, but there are various algorithms like [Kalman filter](https://en.wikipedia.org/wiki/Kalman_filter), [Particle filter](https://en.wikipedia.org/wiki/Particle_filter), and [GraphSLAM](https://people.eecs.berkeley.edu/\~pabbeel/cs287-fa13/slides/GraphSLAM.pdf) that help provide an approximate solution in certain environments to both these problems.

The general idea of slam can be subdivided into different stages:

* Landmark Extraction
* Data Association
* State Estimation
* State Update
* Landmark Update

![](/ERC-website-2021/static/slam_image11.jpg)  
\*_In the image above, EKF stands for Extended Kalman Filter, an algorithm used for implementing SLAM._

SLAM is an idea through which we estimate the robot’s state through its controls, and using the locations of the landmarks we witness, we improve the estimate of the robot's state. It is based on a probabilistic model, where each item has a probability of being in a particular position.

# Applications of SLAM

![](/ERC-website-2021/static/slam_image10.png)

SLAM is used extensively in various indoor, outdoor, aerial, underwater and underground applications for both manned and unmanned vehicles.

For e.g. Reef monitoring, exploration of mines, surveillance drones, terrain mapping etc.

# Probabilistic Interpretation of SLAM

In the probabilistic world, each measurement and estimate has some error associated with it, and we can only determine a probability distribution to estimate the map and localisation of a robot using SLAM. Mathematically, it can be represented as:

![](/ERC-website-2021/static/slam_image14.png)

This means that the objective of SLAM is to obtain the probability distribution of the robot’s path and a map of its surroundings using the knowledge of the robot’s controls and the observations it makes using its sensors.

Below is a graphical representation of SLAM. **xt** is the location of the robot at time t, **m** represents the map, **ut** represents the controls of the robot at time t, and **zt** represents the values observed by the sensors on the robot.  
![](/ERC-website-2021/static/slam_image6.png)

# Homogeneous Coordinates

In SLAM, cameras are often used as sensors to obtain information about the robot's surroundings. Cameras don’t capture a 3D image, rather they capture a projection of the 3D world. The mathematical formulations can become simpler if we use projective geometry instead of euclidean geometry. The system of coordinates used in projective geometry is called homogeneous coordinates. The details regarding the mathematics of homogeneous coordinates can be found [here](https://en.wikipedia.org/wiki/Homogeneous_coordinates).

# Bayes Filter

A lot of the different models used for SLAM such as the Kalman Filter and the Particle Filter are based on the Recursive Bayes Filter. In the Bayes filter, the **belief** of **xt** is defined as

![](/ERC-website-2021/static/slam_image8.png)

The recursive Bayes Filter can then be defined as a 2 step process:

* Prediction Step

  ![](/ERC-website-2021/static/slam_image12.png)
* Correction Step  
  ![](/ERC-website-2021/static/slam_image1.png)

**_p_(_xt | ut_, _xt-1_)** represents the motion based model, which is the distribution of the current location based on the robot’s controls and its previous location. **_p_(_zt_ | _xt_)** represents the correction introduced based on the sensor readings **_zt_**. This Bayes filter acts as a framework for different realizations such as the Kalman Filter and the Particle Filter. For further details regarding the Bayes Filter, refer [here](https://en.wikipedia.org/wiki/Recursive_Bayesian_estimation).

# Motion Models

In the section of Bayes Filter, we saw the term **_p_(_xt | ut_ , _xt-1_)** represents the motion based model. In general, there are 2 common types of motion based models:

* Odometry based model
* Velocity based model

The Odometry based model is mainly used for those robots that have wheel encoders, i.e. where it is feasible to count wheel motions and find the direction of motion. The Velocity based model is normally used where the odometry based model cannot be implemented, e.g. a drone does not have wheels and wheel encoders cannot be used. For a detailed description of the 2 models here including their mathematical formulations, check [this](https://ccc.inaoep.mx/\~mdprl/documentos/CH5.pdf) document.

# Sensor Models

The term **_p_(_zt_ | _xt_** **)** represents the sensor based model. It represents the probability distribution of getting a measurement **_zt_** at a position **_xt ._** There can be different kinds of sensors used.

* Internal sensors such as gyroscopes, accelerometers etc
* Proximity sensors such as Sonar, Radar etc.
* Visual Sensors like cameras
* Satellite based sensors like GPS

For more details regarding the Sensor Models, refer to [this](http://ais.informatik.uni-freiburg.de/teaching/ss09/robotics/slides/e_sensor-models.pdf) document.

![](/ERC-website-2021/static/slam_image2.jpg)

# Filters

There are 2 main methods used for implementing SLAM, that is the Kalman Filter and the Particle Filter. They are based on the Bayes Filter and use the motion and sensor models to get a good estimate for SLAM.

# The Kalman Filter

The Kalman filter is a filter based on the Bayes filter, and is the optimal solution for the linear Gaussian case. It assumes all probability distributions are gaussian. For a complete tutorial on Kalman filter, check [here](https://www.kalmanfilter.net/default.aspx). In short, the Kalman filter can be depicted as follows:

![](/ERC-website-2021/static/slam_image3.png)![](/ERC-website-2021/static/slam_image5.png)

# Particle Filter

The particle filter is also based on the Bayes filter, but it is superior to the Kalman filter in non-linear and non-Gaussian systems. The particle filter models by samples, and the more samples, the better the distribution.

![](/ERC-website-2021/static/slam_image4.png)![](/ERC-website-2021/static/slam_image7.png)  
For more details regarding the particle filter, check [here](https://en.wikipedia.org/wiki/Particle_filter) or [here](http://ais.informatik.uni-freiburg.de/teaching/ws13/mapping/pdf/slam11-particle-filter.pdf).

# Further Reading

For tutorials on the Kalman Filter: check [here](http://www.kalmanfilter.net) or [here](https://www.bzarg.com/p/how-a-kalman-filter-works-in-pictures/).

For a reading on the Particle Filter: check [here](https://towardsdatascience.com/particle-filter-a-hero-in-the-world-of-non-linearity-and-non-gaussian-6d8947f4a3dc) or the resources mentioned in the particle filter section.

For a reading on the Extended Kalman Filter, check [here](https://en.wikipedia.org/wiki/Extended_Kalman_filter).

For a complete course on SLAM including slides and recordings from the University of Freiburg, check [here](http://ais.informatik.uni-freiburg.de/teaching/ws13/mapping/).