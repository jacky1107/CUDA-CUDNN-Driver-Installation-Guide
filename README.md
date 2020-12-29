# Cuda-Toolkit / Cudnn / NVIDIA-Driver Installation

In order to install cuda/cudnn/nvidia-driver on ubuntu 18.04/20.4, you can follow these steps below. (cuda-toolkit-archive and official documentation can find in here: <https://developer.nvidia.com/cuda-toolkit-archive>)

## System Requirements

1. Verify your graphics card is from NVIDIA and it is listed in <https://developer.nvidia.com/cuda-gpus>, your GPU is CUDA-capable.

2. Verify you have a supported version of linux

   ```bash
   uname -m && cat /etc/*release
   ```

   You should see output similar to the following, modified for your particular system:

   `x86_64 Red Hat Enterprise Linux Workstation release 6.0 (Santiago)`

   The x86_64 line indicates you are running on a 64-bit system. The remainder gives information about your distribution.

3. Verify the system has gcc installed

   To verify, type the following on the command line:

   ```bash
   gcc --version
   ```

   If an error message displays, type the following on the command line:

   ```bash
   sudo apt upgrade
   sudo apt update
   sudo apt install gcc
   ```

4. Verify the system has the correct kernel headers and development packages installed.

   The kernel headers and development packages for the currently running kernel can be installed with:

   `sudo apt-get install linux-headers-$(uname -r)`

## Remove nvidia-driver/cuda/cudnn completly

Type the following at the command line step by step can remove it completly. (If an error message displays, that means you don't have nvidia-driver/cuda/cudnn installed, that's great)

```bash
sudo apt-get purge nvidia*
sudo apt-get autoremove
sudo apt-get autoclean
sudo rm -rf /usr/local/cuda*
sudo /usr/local/cuda-X.Y/bin/uninstall_cuda_X.Y.pl
sudo /usr/bin/nvidia-uninstall
```

## Install Cuda-Toolkit and nvidia-driver

1. Verify the cuda version by the computational ability of GPU: <https://zh.wikipedia.org/zh-tw/CUDA>

2. Find the correct cuda-toolkit-archive: <https://developer.nvidia.com/cuda-toolkit-archive>

3. Choose the correct version of ubuntu and 32-bit/64-bit system

4. In the last step, you will see these options: .run / .deb(local) / .deb(network) / ...

   Select the .deb(local), and download it by following steps (But the step 5 is little different than the documentation).

   For example (cuda-10.1):

   ```bash
   1. Download the .deb file
   2. sudo dpkg -i cuda-repo-ubuntu1804-10-1-local-10.1.105-418.39_1.0-1_amd64.deb
   3. sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
   4. sudo apt-get update
   5. sudo apt-get install cuda-10.1
   ```

5. Add the path in .bashrc file

   ```bash
   export PATH=$PATH:/usr/local/cuda/bin
   export LD_LIBRARY=$LD_LIBRARY:/usr/local/cuda/lib64
   ```

## Verify the versoin of Cuda-Toolkit / NVIDIA-Driver

Verify the driver version by typing `nvidia-smi`

Verify the cuda version by typing `nvcc -V`

## Install Cudnn

1. Find the correct cuda-toolkit-archive: <https://developer.nvidia.com/rdp/cudnn-archive>
2. Choose the correct version according to cuda
3. Here you have 3 libraries to installed.

   For example(ubuntu 18.04/cuda-10.1):

   - cuDNN Runtime Library for Ubuntu18.04 x86_64 (Deb)

   - cuDNN Developer Library for Ubuntu18.04 x86_64 (Deb)

   - cuDNN Code Samples and User Guide for Ubuntu18.04 x86_64 (Deb)

## Verify the Cudnn Install (v7/v8)

```bash
cp -r /usr/src/cudnn_samples_v8/ $HOME`
cd $HOME/cudnn_samples_v8/mnistCUDNN`
make clean && make`
./mnistCUDNN`
```

If cuDNN is properly installed and running on your Linux system, you will see a message similar to the following:

`Test passed!`

## Install OpenPose

### Clone OpenPose

```bash
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
cd openpose/
git submodule update --init --recursive --remote
```

### Install Dependancy

```bash
sudo apt-get install protobuf-compiler libprotobuf-dev
sudo apt-get install libgoogle-glog-dev
sudo apt-get install libopencv-dev
sudo apt-get install libboost-all-dev
sudo apt-get install libhdf5-dev
sudo apt-get install libatlas-base-dev
sudo apt-get install libzbar0
```

### Install Cmake

Go to: <https://cmake.org/download/> (If want to choose previous version, then go to following link: "https://cmake.org/files/", v3.15 or above version is great)

Reference: <https://askubuntu.com/questions/829310/how-to-upgrade-cmake-in-ubuntu>

```bash
sudo apt remove cmake
Download cmake-<version>.sh to ${CMAKE_PATH}
sudo cp -r ${CMAKE_PATH}/cmake-<version>.sh /opt
sudo bash /opt/${CMAKE_PATH}/cmake-<version>.sh
sudo ln -s /opt/${CMAKE_PATH}/cmake-<version>/bin/* /usr/local/bin
```

### CMake Configuration

1. Go to the OpenPose folder and open CMake-GUI from it

   ```bash
   cd {OpenPose_folder}
   mkdir build/
   cd build/
   cmake-gui ..
   ```

2. Press the `Configure` button, keep the generator in Unix Makefiles (Ubuntu).
3. Enabling Python (optional step, only apply it if you plan to use the Python API): Enable the `BUILD_PYTHON` flag and click `Configure` again.
4. Press the `Generate` button and proceed to `Compilation`. You can now close CMake.

### Compilation

Run the following commands in your terminal.

```bash
cd build/
make -j`nproc`
```

### TEST

```bash
cd build/examples/tutorial_api_python/
python openpose_python.py
```
