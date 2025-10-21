
# Ubuntu System install

## Reference
1. [Ubuntu20.04双系统安装详解（内容详细，一文通关！）](https://blog.csdn.net/wyr1849089774/article/details/133387874)
2. [Windows 和 Ubuntu 双系统的安装和卸载](https://www.bilibili.com/video/BV1554y1n7zv?spm_id_from=333.788.recommend_more_video.0&vd_source=ca57ff13f14c6081a999b764e6f075ec)
3. [https://blog.csdn.net/ShakalakaPHD/article/details/107965680](https://blog.csdn.net/ShakalakaPHD/article/details/107965680)

# Ubuntu commonly used  software

```bash
# vscode
# https://code.visualstudio.com/Download
# 永久关闭自动激活 base 环境
conda config --set auto_activate_base false 

# terminitor
sudo apt update
sudo apt install terminator

# obsidian(通过Snap安装)
sudo snap install obsidian --classic 

# flameshot
sudo apt install flameshot 

# gitkraken
wget https://release.axocdn.com/linux/gitkraken-amd64.deb
sudo dpkg -i gitkraken-amd64.deb

# clash
https://www.mgodmonkey.cn/posts/a5d6f412.html
sudo mv Clash\ for\ Windows-0.20.39-x64-linux /opt/clash
cd /opt/clash  
./cfw

# time sync
sudo apt update
sudo apt install ntpdate
sudo ntpdate time.windows.com
sudo hwclock --localtime --systohc 

```

## Reference
1. [ubuntu 20.04 安装截图工具 flameshot](https://blog.csdn.net/qq_45642410/article/details/111054365) 
2. [ubuntu初始配置——安装配置截图工具flameshot](https://juejin.cn/post/7345350913655816218)
3. [ubuntu初始配置——汇总](https://juejin.cn/user/398498625489867/posts)
4. [Linux/Ubuntu 安装图形界面版 clash-gui](https://www.mgodmonkey.cn/posts/a5d6f412.html)




# Nvidia Driver


## Reference
1. [【超详细】【ubunbu 22.04】 手把手教你安装nvidia驱动，有手就行，隔壁家的老太太都能安装_ubuntu安装nvidia显卡驱动-CSDN博客](https://blog.csdn.net/huiyoooo/article/details/128015155)
2. [[2025-03-20#一、Nidia显卡驱动(apt install)]]

# CUDA

## deb
```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600

wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb

sudo cp /var/cuda-repo-ubuntu2004-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
# sudo cp /var/cuda-repo-ubuntu2004-11-8-local/cuda-368EAC11-keyring.gpg /usr/share/keyrings/

sudo apt-get update
sudo apt-get -y install cuda
```
## run
```bash
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run
sudo sh cuda_11.8.0_520.61.05_linux.run

```

[[2025-03-20#二、CUDA(`run`文件安装)]]

## Reference
1. [[2025-03-20#二、CUDA(`run`文件安装)]]
2. [https://developer.nvidia.com/cuda-toolkit-archive](https://developer.nvidia.com/cuda-toolkit-archive)


# CUDNN

## deb
```bash
sudo dpkg -i cudnn-local-repo-ubuntu2004-8.9.0.131_1.0-1_amd64.deb
sudo cp /var/cudnn-local-repo-ubuntu2004-8.9.0.131/cudnn-*-keyring.gpg /usr/share/keyrings/

sudo apt-get update 
# sudo apt-get -y install cudnn
sudo apt-get install libcudnn8 libcudnn8-dev libcudnn8-samples


# 验证是否安装成功
cp -r /usr/src/cudnn_samples_v8 $HOME
cd ~/cudnn_samples_v8/mnistCUDNN
make -j
./mnistCUDNN

# option:查看本地仓库中提供的所有 cudnn 包
apt-cache search cudnn
```

## Reference
1. [[2025-03-20#三、CUDNN]]]
2. [https://developer.nvidia.com/rdp/cudnn-archive](https://developer.nvidia.com/rdp/cudnn-archive)


# TensorRT

## deb
```bash
# sudo dpkg -i nv-tensorrt-local-repo-ubuntu2004-8.6.0-cuda-11.8_1.0-1_amd64.deb
# sudo cp /var/nv-tensorrt-local-repo-ubuntu2004-8.6.0-cuda-11.8/*-keyring.gpg /usr/share/keyrings/
sudo dpkg -i nv-tensorrt-local-repo-ubuntu2004-8.6.1-cuda-11.8_1.0-1_amd64.deb 


sudo apt-get update
sudo apt-get install tensorrt

# 验证
dpkg -l | grep TensorRT
```


## Reference
1. [[2025-03-20#四、TensorRT]]
2. [https://www.cnblogs.com/asnelin/p/16102862.html](https://www.cnblogs.com/asnelin/p/16102862.html)
3. https://docs.nvidia.com/deeplearning/tensorrt/latest/installing-tensorrt/installing.html

# Docker

## 安装Docker

``` bash
# 更新索引
sudo apt update 

# 安装Docker依赖
sudo apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common  

# 添加Docker的官方GPG密钥(清华源)
curl -fsSL https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg 

# 添加Docker的官方APT仓库
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null 

# 安装Docker Engine-Community
sudo apt-get update
sudo apt install docker-ce 

# 验证是否安装成功
sudo docker --version 

# 将当前用户添加到docker组（以便无需sudo运行Docker命令）
sudo groupadd docker
sudo gpasswd -a ${USER} docker
sudo service docker restart
newgrp - docker

# 如果遇到权限问题，尝试:
sudo chmod o+rw /var/run/docker.sock

```

## 安装NVIDIA容器运行时
1. 离线安装教程 
2. 在线安装教程 
```bash

# 添加Nidia仓库
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

# 更新索引
sudo apt-get update

# 安装ToolKit
sudo apt-get install -y nvidia-container-toolkit

# 配置Nvidia 容器运行时
sudo nvidia-ctk runtime configure --runtime=docker

# 安装完成后重启docker使nvidia生效. 使用下列命令重启docker
sudo systemctl restart docker.service

# option: 使用下列命令验证显卡是否docker中可备加载
sudo docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi
```



## Reference:
1. [https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)


# ROS

# PCL
## APT

```bash

sudo apt update
sudo apt install libpcl-dev

pcl_version  # 部分系统支持此命令，或者
dpkg -s libpcl-dev | grep Version

```

## 源码编译
...


# OpenCV
## APT

```bash
sudo apt update
sudo apt install libopencv-dev


```

## 源码编译
...
