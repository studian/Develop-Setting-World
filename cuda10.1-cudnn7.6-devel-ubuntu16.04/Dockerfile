FROM nvidia/cuda:10.1-devel-ubuntu16.04

LABEL maintainer "NVIDIA CORPORATION <cudatools@nvidia.com>"

ENV CUDNN_VERSION 7.6.4.38
LABEL com.nvidia.cudnn.version="${CUDNN_VERSION}"

RUN apt-get update && apt-get install -y --no-install-recommends \
    libcudnn7=$CUDNN_VERSION-1+cuda10.1 \
libcudnn7-dev=$CUDNN_VERSION-1+cuda10.1 \
&& \
    apt-mark hold libcudnn7 && \
    rm -rf /var/lib/apt/lists/*
##########################################################

# optional, if the default user is not "root", you might need to switch to root here and at the end of the script to the original user again.
# e.g.
# USER root
##########################################################################################3
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y upgrade
RUN apt-get install -y screen terminator tmux vim wget
RUN apt-get install -y aptitude build-essential cmake g++ gfortran git pkg-config software-properties-common
RUN apt-get install -y unrar wget curl
RUN apt-get install -y ffmpeg
RUN apt-get install -y gnuplot-x11
RUN apt-get install -y python3 python3-dev python3-pip
RUN python3 -m pip install --upgrade pip
RUN python3 -m pip install --upgrade setuptools wheel cython
RUN python3 -m pip install --upgrade numpy h5py dill matplotlib mock protobuf tqdm

#Bazel
RUN apt-get install -y openjdk-8-jdk
RUN apt-get install -y pkg-config zip g++ zlib1g-dev unzip python
RUN mkdir -p /pkg/bazel
WORKDIR /pkg/bazel
RUN wget https://github.com/bazelbuild/bazel/releases/download/0.26.1/bazel-0.26.1-installer-linux-x86_64.sh
RUN chmod a+x bazel-0.26.1-installer-linux-x86_64.sh
RUN ./bazel-0.26.1-installer-linux-x86_64.sh
##########################################################################################3
RUN apt-get update && apt-get install -y --no-install-recommends \
        pkg-config \
        libxau-dev \
        libxdmcp-dev \
        libxcb1-dev \
        libxext-dev \
        libx11-dev && \
    rm -rf /var/lib/apt/lists/*

# replace with other Ubuntu version if desired
# see: https://hub.docker.com/r/nvidia/opengl/
# e.g. nvidia/opengl:1.1-glvnd-runtime-ubuntu16.04)
COPY --from=machinekoder/nvidia-opengl-docker:1.1-glvnd-runtime-stretch \
  /usr/local/lib/x86_64-linux-gnu \
  /usr/local/lib/x86_64-linux-gnu

# replace with other Ubuntu version if desired
# see: https://hub.docker.com/r/nvidia/opengl/
# e.g. nvidia/opengl:1.1-glvnd-runtime-ubuntu16.04
COPY --from=machinekoder/nvidia-opengl-docker:1.1-glvnd-runtime-stretch \
  /usr/local/share/glvnd/egl_vendor.d/10_nvidia.json \
  /usr/local/share/glvnd/egl_vendor.d/10_nvidia.json

RUN echo '/usr/local/lib/x86_64-linux-gnu' >> /etc/ld.so.conf.d/glvnd.conf && \
    ldconfig && \
    echo '/usr/local/$LIB/libGL.so.1' >> /etc/ld.so.preload && \
    echo '/usr/local/$LIB/libEGL.so.1' >> /etc/ld.so.preload

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics


RUN apt-get update && \
        apt-get install -y \
        wget \
        zlib1g-dev \
        libssl-dev \
        curl\
        build-essential \
        cmake \
        git \
        wget \
        unzip \
        yasm \
        pkg-config \
        libswscale-dev \
        libtbb2 \
        libtbb-dev \
        libjpeg-dev \
        libpng-dev \
        libtiff-dev \
        libavformat-dev \
        libpq-dev \
        libgl1-mesa-glx \
        vim

# install miniconda
RUN wget https://repo.continuum.io/miniconda/Miniconda3-4.5.11-Linux-x86_64.sh -O Miniconda.sh && \
	/bin/bash Miniconda.sh -b -p /opt/conda && \
	rm Miniconda.sh

ENV PATH /opt/conda/bin:$PATH
RUN ln -s /opt/conda/bin/pip /opt/conda/bin/pip3

# setup python
RUN conda install python=3.6

# install tensorflow, pytorch, keras
#RUN pip3 install --upgrade pip && \
#        pip3 install --no-cache-dir\
#        torch==0.4.1 \
#        torchvision \
#        numpy \
#	opencv-contrib-python

ENV LANG C.UTF-8

WORKDIR /

