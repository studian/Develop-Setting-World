# 라즈베리파이3 모델B + 우분투 Mate 16.04 + ROS Kinetic 설치

sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116
sudo apt-get update
sudo apt-get install ros-kinetic-ros-base

sudo rosdep init
rosdep update

gedit ~/.bashrc (.bashrc 파일에 하기의 내용을 적고 저장)
```````````````````````````````````````````````````````````````````````
# set ROS Kinetic
source /opt/ros/kinetic/setup.bash
source ~/catkin_ws/devel/setup.bash

# set ROS Network
export ROS_MASTER_URI=http://localhost:11311
export ROS_HOSTNAME=localhost

# set ROS alias command
alias cw='cd ~/catkin_ws'
alias cs='cd ~/catkin_ws/src'
alias cm='cd ~/catkin_ws && catkin_make'
````````````````````````````````````````````````````````````````````````````

source ~/.bashrc

sudo apt-get install python-rosinstall

mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
cd ~/catkin_ws/
catkin_make
(sudo apt-get install ros-kinetic-turtlesim)

(sudo apt-get install chromium-browser)
