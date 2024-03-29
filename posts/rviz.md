---
title: Rviz
author: Jacob Thomas Sony
hero_image: "/ERC-website-2021/static/rviz_cover.jpg"
date: 2021-10-17T12:30:00Z

---
Rviz is a **3D visualizer** for **ROS** that lets us view a lot about the **sensing**, **processing** and **state** of a robot.  
This make the development of robots easier and also enables us to debug more efficiently (better than looking at numbers on a terminal :P)

## Rviz vs Gazebo

Rviz is a **visualizer** i.e it shows what the robot perceives is happening while Gazebo is a **simulator** i.e. it shows what is actually happening.  
Consider the scenario in which we do not have physical hardware-based robots. In that case we would use a simulator like Gazebo to know what would actually happen and the data from the sensors can be visualized in a visualization tool like Rviz. In case we have physical robots, then the data from the sensors can still be visualized in Rviz, but we do not need a simulator necessarily.

To get started with the installation and some beginner friendly example in Rviz, you may follow [_this link_](https://colab.research.google.com/drive/1FY9xGYzi_hh2C5L747Im7VsMwvI352MK#scrollTo=mKydxDSjsMCr).