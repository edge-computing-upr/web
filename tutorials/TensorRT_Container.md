# TensorRT TensorFlow Container Setup Guide

## Prerequisites
Before starting, ensure your system meets these requirements:
- Linux operating system (Ubuntu 20.04 or later recommended)
- Apropriate NVIDIA GPU
- Apropriate NVIDIA driver 
- At least 10GB of free disk space

## Table of Contents
1. [Install NVIDIA Driver](#install-nvidia-driver)
2. [Install Docker](#install-docker)
3. [Install NVIDIA Container Toolkit](#install-nvidia-container-toolkit)
4. [Install TensorRT Container](#install-tensorrt-container)
5. [Verification](#verification)
6. [Troubleshooting](#troubleshooting)

## Install NVIDIA Driver

1. Check if NVIDIA driver is installed:
```bash
nvidia-smi
```

2. Install [NVIDIA drivers](https://docs.nvidia.com/datacenter/tesla/driver-installation-guide/index.html):
```bash
sudo apt install nvidia-driver-###  # Use latest recommended version
sudo reboot
```

## Install Docker

1. Check if docker is install and remove old versions (if any):
```bash
dpkg -l | grep -i docker

```
2. Install [Docker Engine](https://docs.docker.com/engine/):
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

3. Verify Docker installation:
```bash
sudo docker run hello-world
```

## Install NVIDIA Container Toolkit

1. Install [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) (if necessary):

## Install TensorRT Container

1. Pull the TensorRT container with [TensorFlow support](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/tensorflow/tags):
```bash
sudo docker pull nvcr.io/nvidia/tensorflow:##.##-tf#-py3
```

2. Run the container:
```bash
sudo docker run --gpus all -it --rm nvcr.io/nvidia/tensorflow:##.##-tf#-py3
```

## Verification

1. Inside the container, verify TensorFlow can see the GPU:
```python
import tensorflow as tf
print("Num GPUs Available: ", len(tf.config.list_physical_devices('GPU')))
```

2. Verify TensorRT:
```python
import tensorflow as tf
from tensorflow.python.compiler.tensorrt import trt_convert as trt
print(tf.__version__)
```

## Troubleshooting

### Common Issues and Solutions

1. **Docker permission denied**

2. **NVIDIA driver not found**
```bash
sudo reboot
```

3. **Container fails to start with GPU error**
```bash
# Check if NVIDIA runtime is properly configured
sudo docker info | grep -i runtime
```

## Additional Resources

- [NVIDIA Container Toolkit Documentation](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/overview.html)
- [TensorRT Documentation](https://docs.nvidia.com/deeplearning/tensorrt/developer-guide/index.html)
- [Docker Documentation](https://docs.docker.com/)

---
*Note: Version numbers in this guide may need to be updated based on your system requirements and the latest available versions.*