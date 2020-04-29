* reference of install ROS-Kinetic-full: 
* reference of install cuda 9.0: https://yangcha.github.io/CUDA90/
* reference of autoware: https://gitlab.com/autowarefoundation/autoware.ai/autoware/-/wikis/Source-Build

### 1. install ROS-Kinetic-full on Ubuntu 16.04

### 2. install cuda 9.0 on Ubuntu 16.04

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
* Set up the development environment by modifying the PATH and LD_LIBRARY_PATH variables, also add them to the end of .bashrc file:
```
PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}
LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

### 3. install Autoware 1.12.0 with cuda on Ubuntu 16.04
