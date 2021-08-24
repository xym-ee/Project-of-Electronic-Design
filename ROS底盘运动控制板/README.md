# MIMXRT1020-motion-control-board
本项目包含运动控制板和一个简单的遥控器。
本项目是一个轮式ROS机器人项目的子项目，该控制板作为ROS中的一个节点，接收控制消息，驱动轮式底盘。遥控器直接用于底盘驱动、优先级高于ROS消息。（未来可能会把完整项目全放上来）

## 运动控制板
NXP i.MX RT1021 MCU的控制板，双层PCB设计。
运动控制板是轮式机器人系统系统底层硬件的核心，它不但直接对执行机构进行驱动控制，而且可以对各种底层资源进行管理。包含运动控制板的整个底层移动平台是一个相对独立的系统，只对外部留出了一个串行通信的控制接口，对于上层的运行复杂算法的工控机来说，底层移动平台是一个黑盒，是整个软件系统中的一个节点，这个节点发布里程计信息，订阅车模转角与速度信息。

<img src="./pictures/运动控制板总体设计图.jpg" width="400px" align="middle"/>

<br>

<img src="./pictures/运动控制板PCB设计图.jpg" width="400px" align="middle"/>

<br>

<img src="./pictures/运动控制板实物图.jpg" width="400px" align="middle"/>


## 简单遥控器

<img src="./pictures/遥控器PCB设计图.jpg" width="400px" align="middle"/>


