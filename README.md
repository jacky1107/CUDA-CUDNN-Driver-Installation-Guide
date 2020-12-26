# CUDA_CUDNN_DRIVER_Installation

In order to install cuda/cudnn/nvidia-driver on ubuntu 18.04/20.4, you can follow these steps below.

-   If your graphics card is from NVIDIA and it is listed in https://developer.nvidia.com/cuda-gpus, your GPU is CUDA-capable.
-   Verify you have a supported version of linux `uname -m && cat /etc/*release`

https://developer.nvidia.com/cuda-toolkit-archive

# Remove nvidia-driver and cuda completly

`sudo apt-get purge nvidia*`
`sudo apt-get autoremove`
`sudo apt-get autoclean`
`sudo rm -rf /usr/local/cuda*`

https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html

1. Verify you have a cuda-capable GPU

`lspci | grep -i nvidia`

2. Verify you have a supported version of linux

`uname -m && cat /etc/*release`

`sudo /usr/local/cuda-X.Y/bin/uninstall_cuda_X.Y.pl`
`sudo /usr/bin/nvidia-uninstall`
`sudo apt-get --purge remove <package_name>`

`sudo apt upgrade`
`sudo apt update`
`sudo apt install gcc`
`sudo apt-get install linux-headers-$(uname -r)`

# Install Cmake

https://askubuntu.com/questions/829310/how-to-upgrade-cmake-in-ubuntu

Go to: https://cmake.org/download/ (If want to choose previous version, then go to: "https://cmake.org/files/")
And find v3.15 or above version.

`sudo apt remove cmake`
`sudo cp -r ${CMAKE_PATH}/cmake-<version>.sh /opt`
`sudo bash /opt/${CMAKE_PATH}/cmake-<version>.sh`
`sudo ln -s /opt/${CMAKE_PATH}/cmake-<version>/bin* /usr/local/bin`

# Install Dependancy

`sudo apt-get install protobuf-compiler libprotobuf-dev`
`sudo apt-get install libgoogle-glog-dev`
`sudo apt-get install libopencv-dev`
`sudo apt-get install libboost-all-dev`
`sudo apt-get install libhdf5-dev`
`sudo apt-get install libatlas-base-dev`
`sudo apt install libzbar0`
