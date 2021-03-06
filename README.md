# ROS Packages for Scout Mobile Robot

## Packages

This repository contains minimal packages to control the scout robot using ROS. 

* scout_bringup: launch and configuration files to start ROS nodes 
* scout_base: a ROS wrapper around [wrp_sdk](https://github.com/westonrobot/wrp_sdk) to monitor and control the scout robot
* scout_msgs: scout related message definitions

## Communication interface setup

Please refer to the [README](https://github.com/westonrobot/wrp_sdk#hardware-interface) of "wrp_sdk" package for setup of communication interfaces.

#### Note on CAN interface on Nvidia Jetson Platforms

Nvidia Jeston TX2/Xavier/XavierNX have CAN controller(s) integrated in the main SOC. If you're using a dev kit, you need to add a CAN transceiver for proper CAN communication. 

## Basic usage of the ROS package

1. Install dependent libraries

    ```
    $ sudo apt install -y libasio-dev
    $ sudo apt install -y ros-$ROS_DISTRO-teleop-twist-keyboard
    ```

2. Clone the packages into your catkin workspace and compile

    (the following instructions assume your catkin workspace is at: ~/catkin_ws/src)

    ```
    $ cd ~/catkin_ws/src
    $ git clone https://github.com/westonrobot/wrp_sdk.git
    $ git clone https://github.com/westonrobot/scout_base.git
    $ cd ..
    $ catkin_make
    ```

4. Launch ROS nodes
 
* Start the base node for the real robot

    ```
    $ roslaunch scout_bringup scout_minimal.launch
    ```

    or (if you're using a serial port)
        
    ```
    $ roslaunch scout_bringup scout_minimal_uart.launch
    ```

* Start the keyboard tele-op node

    ```
    $ roslaunch scout_bringup scout_teleop_keyboard.launch
    ```

    **SAFETY PRECAUSION**: 

    The default command values of the keyboard teleop node are high, make sure you decrease the speed commands before starting to control the robot with your keyboard! Have your remote controller ready to take over the control whenever necessary. 
