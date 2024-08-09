# About? 
This task is to control the robot arm using ROS1 joint_state_publisher.Joint state publisher is one of the ROS packages that is commonly used to interact with each joint of the robot. The package contains the joint_state_publisher node, which will find the nonfixed joints from the URDF model and publish the joint state values of each joint in the sensor_msgs/JointState message format.

# Steps

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
