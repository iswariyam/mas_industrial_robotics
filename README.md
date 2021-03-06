[![Build Status](https://travis-ci.com/b-it-bots/mas_industrial_robotics.svg?branch=kinetic)](https://travis-ci.com/b-it-bots/mas_industrial_robotics)

## Install Ubuntu
The repository and its related components have been tested under the following Ubuntu distributions:

- ROS Kinetic: Ubuntu 16.04

If you do not have a Ubuntu distribution on your computer you can download it here

     http://www.ubuntu.com/download

## Git - Version Control
### Install Git Software
Install the Git core components and some additional GUI's for the version control:

     sudo apt-get install git-core gitg gitk

### Set Up Git
Now it's time to configure your settings. To do this you need to open a new Terminal. First you need to tell git your name, so that it can properly label the commits you make:

     git config --global user.name "Your Name Here"

Git also saves your email address into the commits you make.

     git config --global user.email "your-email@youremail.com"


### GIT Tutorial
If you have never worked with git before, we recommend to go through the following basic git tutorial:

     http://excess.org/article/2008/07/ogre-git-tutorial/


## ROS - Robot Operating System
### Install ROS
The repository has been tested successfully with the following ROS distributions. Use the link behind a ROS distribution to get to the particular ROS installation instructions.
Alternatively, you can skip this step, as ROS Kinetic is automatically installed by the setup.sh script described in this [section](#Clone-and-compile-the-MAS-industrial-robotics-software).


- ROS Kinetic - http://wiki.ros.org/kinetic/Installation/Ubuntu

NOTE: Do not forget to update your .bashrc!
  

### ROS Tutorials
If you have never worked with ROS before, we recommend to go through the beginner tutorials provided by ROS:

     http://wiki.ros.org/ROS/Tutorials

In order to understand at least the different core components of ROS, you have to start from tutorial 1 ("Installing and Configuring Your ROS Environment") till tutorial 7 ("Understanding ROS Services and Parameters"). 

    
## Clone and compile the MAS industrial robotics software
First of all you have to clone the repository.

    mkdir ~/temp
    cd ~/temp
    git clone git@github.com:b-it-bots/mas_industrial_robotics.git

Navigate into the cloned repository and run setup.sh file.

     ./setup.sh full <optional arg for catkin_ws parent dir>

This script does the following,

* installs ROS, if not previously installed, provided the optional argument full is given
* creates a catkin workspace folder in the directory specified in the argument or by default places it in home directory, i.e. ~/catkin_ws (if it does not exist)
* copies the clone of the mas_industiral_robotics from your ~/temp to \<your folder\>/catkin_ws/src and installs the necessary ros dependencies and other related repositories
* initiates a catkin build in the catkin workspace

Add the following to your bashrc and source your bashrc, so that you need not execute ./setup.sh script each time you open your terminal

     source <your folder>/catkin_ws/devel/setup.bash

If no errors appear everything is ready to use. Great job!

Finally delete the initially cloned mas_industrial_robotics in ~/temp, as all necessary repositories and dependencies are successfully cloned and installed in your catkin workspace

     rm -rf ~/temp/mas_industrial_robotics


### Setting the Environment Variables
#### ROBOT variable
With the ROBOT variable you can choose which hardware configuration should be loaded when starting the robot. The following line will add the variable to your .bashrc:

     echo "export ROBOT=youbot-brsu-1" >> ~/.bashrc
     source ~/.bashrc



#### ROBOT_ENV Variable
The ROBOT_ENV variable can be used to switch between different environments. The following line will add the variable to your .bashrc:
#### Real robot
     echo "export ROBOT_ENV=brsu-c025" >> ~/.bashrc
     source ~/.bashrc
#### Simulation
     echo "export ROBOT_ENV=brsu-c025-sim" >> ~/.bashrc
     source ~/.bashrc



## Bring up the robot and it's basic components
### In Simulation

     roslaunch mir_bringup_sim robot.launch
     
     
In a new terminal you can open the Gazebo GUI to see the environment and the robot

	     rosrun gazebo_ros gzclient

### At the Real Robot

     roslaunch mir_bringup robot.launch
     

## Test the base

     roslaunch mir_teleop teleop_keyboard.launch
     

## Visualize the robot state and sensor data

     rosrun rviz rviz


## Build a map for base navigation

     roslaunch mir_2dslam 2dslam.launch
     

## Use autonomous navigation
### Omni-directional navigation

     roslaunch mir_2dnav 2dnav.launch nav_mode:=dwa

     


Click on the menu bar "File -> Open Config", navigate to "~/indigo/src/mas_industrial_robotics" and select the "youbot.rviz" file.
