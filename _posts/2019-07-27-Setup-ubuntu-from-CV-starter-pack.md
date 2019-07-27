---
title: Ubuntu starter-pack for Computer Vision
tags: Machine-Learning
---

This tutorial for Ubuntu 18.x and computer with Nvidia GPU, install tensorflow-gpu and opencv.
It require you must install specific version of Cuda, CuDnn to use GPU power. Find more on this [link](
https://stackoverflow.com/questions/50622525/which-tensorflow-and-cuda-version-combinations-are-compatible).
Let's start! :muscle:

## 1. Install anaconda
```bash
# Download Anaconda from it's official website:
https://www.anaconda.com/distribution/#download-section

# Execute anaconda downloaded file:
bash Anaconda3-5.2.0-Linux-x86_64.sh 

# Add environment path to use conda everywhere:
PATH=/home/u/anaconda3/bin:$PATH

# Install anaconda-navigator and update:
conda install -c anaconda anaconda-navigator -y
conda update conda
conda update –all

# Create conda environment for tensorflow (example)
conda create -n tf python=3.6 tensorflow-gpu  keras-gpu  tensorflow  keras
conda activate tf
conda deactivate
```

## 2. Install OpenCV 3.6.8
```bash
#Specify OpenCV version
cvVersion="3.6.8"

# Clean build directories
rm -rf opencv/build
rm -rf opencv_contrib/build

# Create directory for installation
mkdir installation
mkdir installation/OpenCV-"$cvVersion"

# Save current working directory
cwd=$(pwd)

sudo apt -y update
sudo apt -y upgrade

# install some os libraries
sudo apt -y remove x264 libx264-dev
 
## Install dependencies
sudo apt -y install build-essential checkinstall cmake pkg-config yasm
sudo apt -y install git gfortran
sudo apt -y install libjpeg8-dev libpng-dev
 
sudo apt -y install software-properties-common
sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
sudo apt -y update
 
sudo apt -y install libjasper1
sudo apt -y install libtiff-dev
 
sudo apt -y install libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev
sudo apt -y install libxine2-dev libv4l-dev
cd /usr/include/linux
sudo ln -s -f ../libv4l1-videodev.h videodev.h
cd "$cwd"
 
sudo apt -y install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
sudo apt -y install libgtk2.0-dev libtbb-dev qt5-default
sudo apt -y install libatlas-base-dev
sudo apt -y install libfaac-dev libmp3lame-dev libtheora-dev
sudo apt -y install libvorbis-dev libxvidcore-dev
sudo apt -y install libopencore-amrnb-dev libopencore-amrwb-dev
sudo apt -y install libavresample-dev
sudo apt -y install x264 v4l-utils
 
# Optional dependencies
sudo apt -y install libprotobuf-dev protobuf-compiler
sudo apt -y install libgoogle-glog-dev libgflags-dev
sudo apt -y install libgphoto2-dev libeigen3-dev libhdf5-dev doxygen

# Install Opencv python
conda activate tf
conda install -c menpo opencv
conda deactivate

# Download opencv and opencv_contrib
git clone https://github.com/opencv/opencv.git
cd opencv
git checkout 3.6
cd ..
 
git clone https://github.com/opencv/opencv_contrib.git
cd opencv_contrib
git checkout 3.6
cd ..

# Compile and install OpenCV with contrib modules
cd opencv
mkdir build
cd build

cmake -D CMAKE_BUILD_TYPE=RELEASE \
            -D CMAKE_INSTALL_PREFIX=$cwd/installation/OpenCV-"$cvVersion" \
            -D INSTALL_C_EXAMPLES=ON \
            -D INSTALL_PYTHON_EXAMPLES=ON \
            -D WITH_TBB=ON \
            -D WITH_V4L=ON \
            -D OPENCV_PYTHON3_INSTALL_PATH=$cwd/OpenCV-$cvVersion-py3/lib/python3.5/site-packages \
        -D WITH_QT=ON \
        -D WITH_OPENGL=ON \
        -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
        -D BUILD_EXAMPLES=ON ..
        
make -j4
make install

# Use Opencv C++
g++ `pkg-config --cflags --libs <OpenCV_Home_Dir>/installation/OpenCV-3.4.4/lib/pkgconfig/opencv.pc` my_sample_file.cpp -o my_sample_file
```

## 3. Install Nvidia driver
There are two way to install nvida driver on ubuntu: GUI or CMD. Find more in this [link](https://www.cyberciti.biz/faq/ubuntu-linux-install-nvidia-driver-latest-proprietary-driver/).
```bash
sudo apt-get install --no-install-recommends nvidia-driver-418
# Reboot. Check that GPUs are visible using the command: nvidia-smi
```

## 4. Add Nvidia package
```bash
Add NVIDIA package repositories
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.0.130-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804_10.0.130-1_amd64.deb
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
sudo apt-get update
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo apt install ./nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo apt-get update
```

## 5. Install CUDA, CuDnn and TensorRT
```bash
# Install development and runtime libraries (~4GB)
sudo apt-get install --no-install-recommends \
    cuda-10-0 \
    libcudnn7=7.6.0.64-1+cuda10.0  \
    libcudnn7-dev=7.6.0.64-1+cuda10.0


# Install TensorRT. Requires that libcudnn7 is installed above.
sudo apt-get update && \        
        && sudo apt-get install -y --no-install-recommends libnvinfer-dev=5.1.5-1+cuda10.0
```
### Conclusion
Well done, if you run above command line without error, you got powerful libraries for computer vision. In this tutorial, we intro how to install packages for computer vision - focus in tensorflow-gpu, with 5 steps:
1. Install Anaconda
2. Install OpenCV
3. Install NVIDIA driver
4. Install NVIDIA packages
5. Install CUDA, CUDNN and TensorRT
Finalyyy, we can enjoy them now!!! :kissing_heart: :kissing_heart: :kissing_heart:

