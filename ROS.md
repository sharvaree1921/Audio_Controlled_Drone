### Writing Publisher-Subscriber file in Python

1] Configuring ROS
Follow: http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment

Environment Setup:

$ source ~/.bashrc
$ source /opt/ros/melodic/setup.bash

Throughout the tutorials you will see references to rosbuild and catkin. These are the two available methods for organizing and building your ROS code. rosbuild is not recommended or maintained anymore but kept for legacy. catkin is the recommended way to organise your code, it uses more standard CMake conventions and provides more flexibility especially for people wanting to integrate external code bases or who want to release their software.

Creating and building a catkin workspace:

$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make

$ source devel/setup.bash

2] Navigating ROS filesystem
Description: This tutorial introduces ROS filesystem concepts, and covers using the roscd, rosls, and rospack commandline tools.
Follow: http://wiki.ros.org/ROS/Tutorials/NavigatingTheFilesystem

inpecting a package: 
$ sudo apt-get install ros-melodic-ros-tutorials

Quick Overview of Filesystem Concepts:
Packages: Packages are the software organization unit of ROS code. Each package can contain libraries, executables, scripts, or other artifacts.

Manifests (package.xml): A manifest is a description of a package. It serves to define dependencies between packages and to capture meta information about the package like version, maintainer, license, etc... 

Filesystem Tools:
Code is spread across many ROS packages. Navigating with command-line tools such as ls and cd can be very tedious which is why ROS provides tools to help you. 

1. rospack allows you to get information about packages. In this tutorial, we are only going to cover the find option, which returns the path to package. 
$ rospack find [package_name]
$ rospack find roscpp

2. roscd is part of the rosbash suite. It allows you to change directory (cd) directly to a package or a stack.
$ roscd <package-or-stack>[/subdir]
$ roscd roscpp
  
Follow the tutorial there itself.






