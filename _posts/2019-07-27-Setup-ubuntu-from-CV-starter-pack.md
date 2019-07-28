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
conda update --all

# Create conda environment for tensorflow (example)
conda create -n tf python=3.6 tensorflow-gpu  keras-gpu  tensorflow  keras
conda activate tf
conda deactivate
```

## 2. Install OpenCV 3.6.8
```bash
https://www.pyimagesearch.com/2018/05/28/ubuntu-18-04-how-to-install-opencv/
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

