# About? 
This task is to control the robot arm using ROS1 joint_state_publisher. Joint state publisher is one of the ROS packages that is commonly used to interact with each joint of the robot. The package contains the joint_state_publisher node, which will find the nonfixed joints from the URDF model and publish the joint state values of each joint in the sensor_msgs/JointState message format.

# Steps
I've followed this [Tutorial](https://www.youtube.com/playlist?list=PLeEzO_sX5H6TBD6EMGgV-qdhzxPY19m12) to complete the task. 
> [!NOTE]
> You might face the same problems I've faced. so check the "Troubleshooting" section here in readme. 

### Create a URDF Model for the Robot Arm 
Define your robot arm in a URDF (Unified Robot Description Format) file. This file describes the physical properties of the robot, including joints and links.
> [!NOTE]
> URDF (Unified Robot Description Format) is an XML format used in ROS (Robot Operating System) to describe the physical configuration of a robot. It includes details about the robot's joints, links, sensors, actuators, and other physical properties. URDF files are essential for simulating and visualizing robots in ROS and for controlling robot movements in real environments.


https://github.com/user-attachments/assets/1b23e3e0-9724-4709-833a-efb4b2334a37



> [!IMPORTANT]
> I will convert SolidWorks assembly to URDF

> [!NOTE]
> While using SolidWorks assembly it is important NOT changing the joints and links limits after subpressing the mates, otherwise, errors will raise.
> [!CAUTION]
> Chaeck how I put the first part "Base" here : 


### Install ROS and Necessary Packages
I did this step in this [Link](https://github.com/Layan002/AI-Task1-Installing-ROS2). Check and follow it if you have not done it yet. 

### Set Up Your Workspace
- Create a catkin workspace if you don't have one already.
``` LINUX
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
source devel/setup.bash
```
> [!NOTE]
> A catkin workspace is a directory in the Robot Operating System (ROS) where you can build, develop, and manage your ROS packages. Catkin is the official build system of ROS, and it is used to compile and link ROS packages.

<img src= "https://github.com/user-attachments/assets/64a55aed-4a21-4a2f-91dd-fa4a3ff6e29d" alt= "img" width = 800>


# Troubleshooting

### Export URDF is not found
You can find it in Tool tap >> (scroll down). <br>

### Reference Sketch does not exist
<img src= "https://github.com/user-attachments/assets/a13d533e-05dd-40aa-9188-3922e739d957" alt= "img" width = 1000>

To solve this problem I've changed the sketch plane to the "top" of the assembly. 
> [!CAUTION]
> If you did as what the tutorial instructor did you may encounter the same problem I've faced. 

Follow the steps I've done in the video below and the URDF export process will work correctly. <br>

https://github.com/user-attachments/assets/ab4b39e4-1e8c-472a-ae8e-a443339fd054





