### 1. install ROS-Kinetic-full on Ubuntu 16.04

* reference of install ROS-Kinetic-full(1): http://wiki.ros.org/kinetic/Installation/Ubuntu
* reference of install ROS-Kinetic-full(2): https://redisle.tistory.com/7

Install ROS Kinetic for Ubuntu 16.04
```
$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
$ sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
```
```
$ sudo apt-get update
```
```
$ sudo apt install ros-kinetic-desktop-full
```
```
$ sudo rosdep init
```
```
$ rosdep update
```

* System dependencies for Ubuntu 16.04 / Kinetic
```
$ sudo apt-get update
$ sudo apt-get install -y python-catkin-pkg python-rosdep ros-$ROS_DISTRO-catkin gksu
$ sudo apt-get install -y python3-pip python3-colcon-common-extensions python3-setuptools python3-vcstool
$ pip3 install -U setuptools
```

### 2. install cuda 9.0 on Ubuntu 16.04

* reference of install cuda 9.0: https://yangcha.github.io/CUDA90/
* reference of install autoware: https://gitlab.com/autowarefoundation/autoware.ai/autoware/-/wikis/Source-Build

The latest version of CUDA is 9.1. However some deep learning frameworks are not yet ready for CUDA 9.1. The installation script of CUDA-9.1 is very similar to this one.

* OS: Ubuntu 16.04 x86_64
* (Optional) Uninstall old version CUDA Toolkit such as:
```
$ sudo apt-get purge cuda
$ sudo apt-get purge libcudnn6
$ sudo apt-get purge libcudnn6-dev
```
* Install CUDA Toolkit 9.0 and cuDNN 7.0 as follows:
```
$ wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_9.0.176-1_amd64.deb
$ wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb
$ wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/libcudnn7-dev_7.0.5.15-1+cuda9.0_amd64.deb
$ wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/libnccl2_2.1.4-1+cuda9.0_amd64.deb
$ wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/libnccl-dev_2.1.4-1+cuda9.0_amd64.deb
$ sudo dpkg -i cuda-repo-ubuntu1604_9.0.176-1_amd64.deb
$ sudo dpkg -i libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb
$ sudo dpkg -i libcudnn7-dev_7.0.5.15-1+cuda9.0_amd64.deb
$ sudo dpkg -i libnccl2_2.1.4-1+cuda9.0_amd64.deb
$ sudo dpkg -i libnccl-dev_2.1.4-1+cuda9.0_amd64.deb
$ sudo apt-get update
$ sudo apt-get install cuda=9.0.176-1
$ sudo apt-get install libcudnn7-dev
$ sudo apt-get install libnccl-dev
```
* Reboot the system to load the NVIDIA drivers.
```
$ sudo reboot
```

### 3. Setting variables of Operation Environment

* After reboot
```
$ echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
```
* Set up the development environment by modifying the PATH and LD_LIBRARY_PATH variables, also add them to the end of .bashrc file:
```
PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}
LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
```
$ source ~/.bashrc
```

### 4. install Autoware 1.12.0 with cuda on Ubuntu 16.04 (How to build For 1.12.0 and Newer)

* reference of install autoware: https://gitlab.com/autowarefoundation/autoware.ai/autoware/-/wikis/Source-Build

Create a workspace
```
$ mkdir -p autoware.ai/src
$ cd autoware.ai
```
Download the workspace configuration for Autoware.AI. 
* For the 1.12.0 release:
```
$ wget -O autoware.ai.repos "https://gitlab.com/autowarefoundation/autoware.ai/autoware/raw/1.12.0/autoware.ai.repos?inline=false"
```
For newer releases, replace 1.12.0 with the version you want to install.
* For the master version (bleeding edge):
```
$ wget -O autoware.ai.repos "https://gitlab.com/autowarefoundation/autoware.ai/autoware/raw/master/autoware.ai.repos?inline=false"
```
* Download Autoware.AI into the workspace.
```
$ vcs import src < autoware.ai.repos
```
Install dependencies using rosdep.
```
$ rosdep update
$ rosdep install -y --from-paths src --ignore-src --rosdistro $ROS_DISTRO
```
Compile the workspace
* With CUDA support
```
$ AUTOWARE_COMPILE_WITH_CUDA=1 colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release
```
* Without CUDA Support
```
$ colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release
```

### 5. Run ROSBAG Demo of Autoware 1.12.0 with cuda on Ubuntu 16.04

* reference of run autoware demo(1): https://gitlab.com/autowarefoundation/autoware.ai/autoware/-/wikis/ROSBAG-Demo
* reference of run autoware demo(2): https://www.youtube.com/watch?v=OWwtr_71cqI&list=PLMV3EZ9zjNbIkOWvjaY2iU8LVC-pUQMOU&index=8
* reference of run autoware demo(3): https://redisle.tistory.com/9?category=1052330 and https://redisle.tistory.com/9?category=1052330

#### Demo data

This demo will need the given 3D map and ROSBAG sample data. Please download the following sample data before running the demo.
* Download the sample 3D pointcloud/vector map data. 
```
$ wget https://autoware-ai.s3.us-east-2.amazonaws.com/sample_moriyama_data.tar.gz
```
* Download the sample data (LiDAR: VELODYNE HDL-32E, GNSS: JAVAD GPS RTK Delta 3) in ROSBAG format or ROSBAG2 format.
```
$ wget https://autoware-ai.s3.us-east-2.amazonaws.com/sample_moriyama_150324.tar.gz 
```
* or (Mirror)
```
$ wget https://autoware-ai.s3.us-east-2.amazonaws.com/sample_moriyama_150324.bag2.tar.gz
```
* Want more data?
* Once the demo goes well, you can visit ROSBAG STORE to get more data. Please also consider your contribution to this data sharing service by uploading your ROSBAG data.

#### Demo run

Assumptions
* Autoware built from source: the demo data and rosbag have been downloaded into the Downloads folder.
* Autoware run from docker image: the demo data and rosbag have been downloaded into the shared_dir folder within the host.

* Create the `.autoware` directory and extract the demo data inside.
```
$ cd ~
$ mkdir .autoware
$ cd .autoware
$ cp ~/Downloads/sample_moriyama_* .
$ tar zxfv sample_moriyama_150324.tar.gz
$ tar zxfv sample_moriyama_data.tar.gz
```
* Run Autoware For Autoware version 1.12.0 and Newer
```
$ cd autoware.ai
$ source install/setup.bash
$ roslaunch runtime_manager runtime_manager.launch
```
