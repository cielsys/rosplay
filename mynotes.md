# Udacity RoboND Project: ROS Robot pick and place
#### SubmissionNotes -ChrisL

****
## Important Notes for review:
* Attempting to use different environment:
    * Mint18 (not Ubuntu 16.04 LTS (Xenial Xerus)) under
    * VirtualBox (not VMWare)
Because I already have a personalized linux environment VM

### ======= ROS Notes ==============
First steps
In different shells or in background
#### ------- Module1: Basic commands
    roscore &
    rosrun turtlesim turtlesim_node &
    rosrun turtlesim turtle_teleop_key
    rosnode list
    rostopic list
    rostopic info /turtle1/cmd_vel
    rosmsg info geomtry_msgs/Twist

### -------- Module2: Catkin basics
    mkdir -p ~/catkin_ws/src
    cd ~/catkin_ws/src
    catkin_init_workspace
    cd ~/catkin_ws
    catkin_make
    cd ~/catkin_ws/src
    git clone https://github.com/udacity/simple_arm_01.git simple_arm
    cd ~/catkin_ws
    catkin_make
    sudo apt-get install ros-kinetic-controller-manager
    source devel/setup.bash
    # My addition:
    # NOPE sudo apt-get install ros-kinetic-simple-arm
    rosdep install simple_arm
    catkin_make
    source devel/setup.bash


#### -------- Module3: HelloNodeControl
(CatkinWSDownload)[https://github.com/udacity/simple_arm_01]

    $ roslaunch simple_arm robot_spawn.launch
    $ rosparam set /arm_mover/max_joint_2_angle 1.57
    $ rosservice call /arm_mover/safe_move "joint_1: 1.1
    joint_2: 1.2"
    $ rqt_image_view /rgb_camera/image_raw

    rosservice call /arm_mover/safe_move "joint_1: 1.1
    > joint_2: 1.2"
    ERROR: Unable to load type [simple_arm/GoToPosition].
    Have you typed 'make' in [simple_arm]?

Fix with `source devel/setup.bash`
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
### --- Environment:
Fixing EnvProblems
* ERROR: `rosdep install simple_arm simple_arm:` results in `Unsupported OS [mint]`
[Fixing OS dep problems](https://answers.ros.org/question/118151/install-ros-on-linux-mint-16/)
[ROS_OS_OVERRIDE](http://wiki.ros.org/ROS/EnvironmentVariables#ROS_OS_OVERRIDE)
(http://naoniloo.blogspot.com/2014/03/ros-hydro-in-linux-mint-installation.html)

Mint18 is based on Ubuntu 16.04 LTS (Xenial Xerus) Linux/KERNEL4.4
export ROS_OS_OVERRIDE=ubuntu:16.04:xenial

(http://wiki.ros.org/kinetic/Installation/Ubuntu)
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu xenial main" > /etc/apt/sources.list.d/ros-latest.list'
    sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
    sudo apt-get update
    sudo apt-get install ros-kinetic-desktop-full
    sudo rosdep init
    rosdep update
    source /opt/ros/kinetic/setup.bash

(https://answers.ros.org/question/40081/rosdep-doesnt-recognize-os/)
    rosdep resolve <key-name> --os=OS_NAME:OS_VERSION
    rosdep install -ay --os=ubuntu:xenial

    # Issues with this command may arise when using a VM. Try, should fix swinging arm
    sudo apt-get install ros-kinetic-gazebo-ros-control

    # Also, rerun next day can't find rospkg, so
    pip install rospkg

    # Oy! Python got switched by conda... so
    conda create -n python2 python=2.7 anaconda
    source activate python2
    # source deactivate
[Or this...in .bashrc](https://github.com/udacity/RoboND-Python-StarterKit/blob/master/doc/linux_ros_anaconda_warning.md)
    # The solution is to unset your PYTHONPATH variable before sourcing your Anaconda environment:
    source /opt/ros/kinetic/setup.bash
    unset PYTHONPATH

(conda install ros on raspi.sh)[https://gist.github.com/mitmul/538315c68c2069f16f11]
(and)[https://gist.github.com/StefanFabian/17fa715e783cd2be6a32cd5bbb98acd9]

### Coding Guidlines

### Links
[VMToBootable](https://github.com/srini-x/RoboND-Kinematics-Project/blob/master/robond_vm_on_a_bootable_usb/port_vm_2_bootable_usb_V2.md)<br />
### ROS Links
(ROSPy wiki)[http://docs.ros.org/kinetic/api/rospy/html/]
[ROSTurtleSimWiki](http://wiki.ros.org/turtlesim)<br />
[ROSCatkinWiki](http://wiki.ros.org/catkin/conceptual_overview)<br />
[ROSCatkinWorkSpaceNaming](http://www.ros.org/reps/rep-0128.html)<br />

### Feedback notes:
Command line instructions : prompt should have path
