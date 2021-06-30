# Robotic Arm
This repository discusses the installation process of Robot Operating System (ROS) for developing a robot arm.

## 1. ROS installation steps:
1. Download a virtual machine program in your computer, e.g., [virtual box](https://www.virtualbox.org/wiki/Downloads). 
2. Identify the ROS version that you will be using, then check the linux requirements. For this project I will be using the [**Melodic**](http://wiki.ros.org/melodic) version of ROS. 
3. Install the appropriate linux version on your virtual machine. For this project: [**Ubuntu 18.04 (Bionic)**](https://releases.ubuntu.com/18.04.5/).
4. After installing Ubuntu on your virtual machine, now we need to install ROS on Ubuntu.
5. Power on your Ubuntu machine, and open the **ternminal**.
6. Inside the terminal write and run the following commands as specified in (http://wiki.ros.org/melodic/Installation/Ubuntu):
   - Setup your sources.list:
   ```
   $ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
   ```
   - Set up your keys:
   ```
   $ curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
   ```
   - Installation:
       - Update the current packages lists:
       ```
       $ sudo apt-get update
       ```
       - Install the recommended version, the Desktop full 
       ```
       $ sudo apt-get install ros-melodic-desktop-full
       ```
   - Environment setup:
   ```
   $ echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
   $ source ~/.bashrc
   ```
   - Dependencies for building packages:
   ```
   $ sudo apt-get install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
   ```
   - Initialize rosdep:
   ```
   $ sudo rosdep init
   $ rosdep update
   ```
   - To check if ROS correctly installed type the following command, if it works then we shall continue to the next step.
   ```
   $ roscore
   ```
## 2. Create your ROS workspace:
  > [Catkin](http://wiki.ros.org/catkin) is included by default when ROS is installed. Catkin can also be installed from source or prebuilt packages. Most users will want to use the prebuilt packages, but installing it from source is also quite simple.
  - To install catkin:
  ```
  $ sudo apt-get install ros-melodic-catkin
  ```
  - Note: Make sure to edit this command based on your ROS version, in this project it is **melodic**.
  ```
  $ mdir -p ~/catkin_workspace/src
  $ cd ~/catkin_workspace/
  $ catkin_make
  ```
## 3. Install robot arm related packages:
In this project we will be using [Smart Methods Robot Arm](https://github.com/smart-methods/arduino_robot_arm) repository:
  ```
  $ cd ~/catkin_workspace/src
  $ git clone https://github.com/smart-methods/arduino_robot_arm
  
  $ sudo apt-get update
  $ rosdep install --from-paths src --ignore-src -r -y
  $ sudo apt-get install ros-melodic-moveit
  $ sudo apt-get install ros-melodic-joint-state-publisher ros-melodic-joint-state-publisher-gui
  $ sudo apt-get install ros-melodic-gazebo-ros-control joint-state-publisher
  $ sudo apt-get install ros-melodic-ros-controllers ros-melodic-ros-control
  ```
  - Note: Make sure to edit these command based on your ROS version, in this project it is **melodic**.
## 4. Add your catkin workspace setups to the .bashrc file:
  ```
   $ echo "source /home/<username>/catkin_workspace/devel/setup.bash" >> ~/.bashrc
   $ source ~/.bashrc
   ```
## 5. Control the robot arm 
We can control the robot arm by either joint_state_publisher or Moveit and kinematics
- Control the robot arm by joint_state_publisher 
  - RViz
  ```
  $ roslaunch robot_arm_pkg check_motors.launch
  ```
  Then the following window will be opened:
  ![alt text](https://github.com/saraalrumih/Smart_methods-Robotic_Arm-ROS/blob/main/robot_arm_rviz.png)
  - Gazebo
  ```
  $ roslaunch robot_arm_pkg check_motors_gazebo.launch
  ```
  Then the following window will be opened:
  ![alt text](https://github.com/saraalrumih/Smart_methods-Robotic_Arm-ROS/blob/main/robot_arm_gazebo.png)
  ## to be completed
  -  ## make python file executable 
  ```
  $ rosrun robot_arm_pkg joint_states_to_gazebo.py
  ```
- Control the robot arm by Moveit and kinematics
  - Then the following window will be opened:
 ![alt text](https://github.com/saraalrumih/Smart_methods-Robotic_Arm-ROS/blob/main/robot_arm_rviz_moveit.png)
