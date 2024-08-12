# About? 
This task is to control the robot arm using ROS1 joint_state_publisher and controlling the robot arm by Moveit and kinematics. Joint state publisher is one of the ROS packages that is commonly used to interact with each joint of the robot. The package contains the joint_state_publisher node, which will find the nonfixed joints from the URDF model and publish the joint state values of each joint in the sensor_msgs/JointState message format.

MoveIt Configuration: First, the robot's URDF (Unified Robot Description Format) model is configured in MoveIt using the MoveIt Setup Assistant. This involves defining the robot's joints, links, and end effectors.

Planning Group: In MoveIt, a planning group is created, representing the set of joints and links you want to control together. For a robot arm, this typically includes all the joints from the base to the end effector.

# Demo


https://github.com/user-attachments/assets/f13a3c4f-5d91-4cd2-ae71-65425a57a74b



# Steps
I've followed this [Tutorial](https://www.youtube.com/playlist?list=PLeEzO_sX5H6TBD6EMGgV-qdhzxPY19m12) to complete the task. 

and also I was using this [documentation](https://github.com/user-attachments/files/16569456/Importing_URDF_Package_from_Soloidworks_in_ROS.pdf) for commands. 

> [!NOTE]
> You might face the same problems I've faced. so check the "Troubleshooting" section here in readme. 

### Exporting URDF model from SolidWorks
Define your robot arm in a URDF (Unified Robot Description Format) file. This file describes the physical properties of the robot, including joints and links.
> [!NOTE]
> URDF (Unified Robot Description Format) is an XML format used in ROS (Robot Operating System) to describe the physical configuration of a robot. It includes details about the robot's joints, links, sensors, actuators, and other physical properties. URDF files are essential for simulating and visualizing robots in ROS and for controlling robot movements in real environments.


https://github.com/user-attachments/assets/1b23e3e0-9724-4709-833a-efb4b2334a37



> [!IMPORTANT]
> I will convert SolidWorks assembly to URDF

> [!NOTE]
> While using SolidWorks assembly it is important NOT changing the joints and links limits after subpressing the mates, otherwise, errors will raise.

> [!CAUTION]
> Check how I put the first part "Base" in the troubleshooting of " Reference Sketch does not exist".


### Install ROS and Necessary Packages
I did this step here [ROS1 installation](https://github.com/Layan002/AI-Task1-Installing-Ubunto-and-ROS). Check and follow it if you have not done it yet. 

### Set Up Your Workspace
- Update and upgrade the system
```
sudo apt update
sudo apt upgrade
```


#### Installing catkin peckage:

```
sudo apt-get install ros-noetic-catkin
```
> [!NOTE]
> Replace noetic with the version of ROS you are using if it differs.

- Source the ROS Setup File
```
source /opt/ros/noetic/setup.bash
```

- Verify Your ROS Installation (Make sure ROS is properly installed and working by checking the version):
```
rosversion -d
```
If this returns a valid ROS version like the output below, your installation is fine.<br>
<img src= "https://github.com/user-attachments/assets/be2a0413-bd4e-4022-9826-6c577de462e3" alt= "img" width = 400>

-  Install catkin_tools (If you're planning to use catkin_tools, you can install it with):
```
sudo apt-get install python3-catkin-tools
```

- Create a catkin workspace if you don't have one already.
  
> [!NOTE]
> A catkin workspace is a directory in the Robot Operating System (ROS) where you can build, develop, and manage your ROS packages. Catkin is the official build system of ROS, and it is used to compile and link ROS packages.

- Update your Ubuntu packages
```
sudo apt-get update
```
- Go to home directory
```
cd ~/
```
- Create a catkin workspace folder along with src folder in it. I am creating a workspace with 
name “moveit_ws”.
```
mkdir --parents moveit_ws/src 
```
> [!NOTE]
> You can use any name for your workspace like “catkin_ws”. 
- Go to the catkin workspace you created. 
```
cd moveit_ws
```
- Initialize the Catkin workspace 
```
 catkin init
```

<img src= "https://github.com/user-attachments/assets/32d28915-629d-4237-9cdb-65eeb3cc7946" alt= "img" width = 400>


- Go to the catkin workspace directory that you created if not already in it.
```
 cd ~/moveit_ws
```
- Build your workspace. 
```
 catkin build 
```
<img src= "https://github.com/user-attachments/assets/fee220e0-21af-4d41-972f-5b5ea8b11e41" alt= "img" width = 400>


- Source the “setup.bash” file automatically generated in your catkin workspace’s “devel” folder 
If you are already in your catkin workspace:
```
 source devel/setup.bash
```
<img src= "https://github.com/user-attachments/assets/3e8bfcdc-ef3a-4522-be3a-999706fdf955" alt= "img" width = 400>

If you are not in your catkin workspace, then give full path:
```
source ~/moveit_ws/devel/setup.bash
```

- Copy robot_arm_urdf and paste it inside src of the moveit_ws
- Open "Cmake.txt" file and copy paste the following inside it:
```
COMPONENTS
 message_generation
roscpp
rospy
std_msgs
geometry_msgs
urdf
xacro
message_generation
```
<img src= "https://github.com/user-attachments/assets/fe07e30e-6a8d-4783-8e52-eb36f40157b7" alt= "img" width = 500>

```
CATKIN_DEPENDS
 geometry_msgs
roscpp
rospy
std_msgs
```
<img src= "https://github.com/user-attachments/assets/05bbd361-c40d-43d7-bd85-89409c623fca" alt= "img" width = 500>

#### Edit "peckage.xml" file.
``` XML
 <build_depend>message_generation</build_depend>
 <build_depend>roscpp</build_depend>
 <build_depend>rospy</build_depend>
 <build_depend>std_msgs</build_depend>
 <build_depend>geometry_msgs</build_depend>
 <build_depend>urdf</build_depend>
 <build_depend>xacro</build_depend>
 <build_depend>std_msgs</build_depend>
 <build_depend>message_generation</build_depend>
```

``` XML
<depend>joint_state_publisher</depend>
```

``` XML
 <depend>moveit_simple_controller_manager</depend>
 <build_export_depend>roscpp</build_export_depend>
 <build_export_depend>rospy</build_export_depend>
 <build_export_depend>std_msgs</build_export_depend>
 <build_export_depend>geometry_msgs</build_export_depend>
 <build_export_depend>urdf</build_export_depend>
 <build_export_depend>xacro</build_export_depend>
 <exec_depend>roscpp</exec_depend>
 <exec_depend>rospy</exec_depend>
 <exec_depend>std_msgs</exec_depend>
 <exec_depend>geometry_msgs</exec_depend>
 <exec_depend>urdf</exec_depend>
 <exec_depend>xacro</exec_depend>
 <exec_depend>message_runtime</exec_depend>
```

<img src= "https://github.com/user-attachments/assets/93ff96c3-2ddf-4cd9-b1d6-8c29210802c6" alt= "img" width = 500>

#### Configure URDF File Generated from SOLIDWORKS for ROS, Gazebo & Moveit Setup Assistant
- In "robot_arm_urdf.urdf" check the lower and upper values for all joints. they should be logically correct. 
<img src= "https://github.com/user-attachments/assets/ba5e3fbe-cea8-4b24-b667-0c60ce69e156" alt= "img" width = 500>

- Add the following to under the name= "robot_arm_urdf">
  
``` URDF

<link name="world"/>
<joint name="base_joint" type="fixed">
    <parent link="world"/>
    <child link="base_link"/>
    <origin rpy="0 0 0" xyz="0.0 0.0 0.17"/>
</joint>

```
- Add this command between last joint and robot tags. In addition, change n to numbers from 1-7 (repeat it for all links from 1-7):
``` URDF
 <transmission name="link_n_trans">
    <type>transmission_interface/SimpleTransmission</type>
    <joint name="joint_n">
    <hardwareInterface>hardware_interface/PositionJointInterface</hardwareInterface>
    </joint>
    <actuator name="link_n_motor">
    <hardwareInterface>hardware_interface/PositionJointInterface</hardwareInterface>
         <mechanicalReduction>1</mechanicalReduction>
    </actuator>
 </transmission>
```
- Add this command between last transmition and robot tags:
``` URDF
<gazebo>
      <plugin name="control" filename="libgazebo_ros_control.so">
            <robotNamespace>/</robotNamespace>
      </plugin>
 </gazebo>
```

- Add this command between last transmition and robot tags. Change n to numbers from 1-7 (repeat it for all links from 1-7):
``` URDF
<gazebo reference="link_n">
     <selfCollide>true</selfCollide>
</gazebo>
```
<img src= "https://github.com/user-attachments/assets/b0d42be8-a3d8-42a4-aabb-022bb1513d92" alt= "img" width = 500>

<img src= "https://github.com/user-attachments/assets/73a1908e-b38e-4af5-94d0-b0784ff834e1" alt= "img" width = 500>


since the instruction is very long I just recommend you to follow the youtube tutorial instead of following my gitHub so I will stop here. 


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





