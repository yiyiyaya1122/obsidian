# Ubuntu System install
## 制作ubuntu系统盘

**1.下载ubuntu镜像**
- [Ubuntu系统下载 | Ubuntu](https://cn.ubuntu.com/download)
- [Index of /ubuntu-releases/20.04/ | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/20.04/)	

**2.下载安装镜像工具**
- [Win32 Disk Imager download | SourceForge.net](https://sourceforge.net/projects/win32diskimager/)

**3.制作ubuntu系统盘**

**4.恢复为u盘**
- [数据恢复软件，硬盘分区工具，系统备份软件 - DiskGenius官方网站](https://www.diskgenius.cn/)

## BUG解决
**1.安装完成没有wifi标志**
- 升级内核、卸载内核
- 安装网卡驱动 
	1. 查看网卡型号[PCI Devices (ucw.cz)](https://admin.pci-ids.ucw.cz/read/PC/10ec/c852 
	2. 手机USB网络共享[Linux通过手机USB网络共享上网 - R-DeepH - 博客园 (cnblogs.com)](https://www.cnblogs.com/R-DeepH/p/15812385.html)
	3. 编译运行驱动[安装ubuntu20.04无法连接wifi问题_ubuntu连不上wifi-CSDN博客](https://blog.csdn.net/qq_51777949/article/details/122807871)
	
## Reference
- [Ubuntu20.04双系统安装详解（内容详细，一文通关！）](https://blog.csdn.net/wyr1849089774/article/details/133387874)
- [Windows 和 Ubuntu 双系统的安装和卸载](https://www.bilibili.com/video/BV1554y1n7zv?spm_id_from=333.788.recommend_more_video.0&vd_source=ca57ff13f14c6081a999b764e6f075ec)
- [Ubuntu20.04安装指南及初步环境配置（超级详细）包含[ROS Noetic、Terminator、Pycahrm等常用工具安装]](https://blog.csdn.net/ShakalakaPHD/article/details/107965680)


# Ubuntu Commands

```bash
# ==================== Ubuntu 常用命令大全 ====================

# 1. 文件目录操作
pwd                      # 显示当前目录
ls -la                   # 详细列表（包含隐藏文件）
cd ~                     # 回家目录
cd -                     # 返回上一个目录

# 2. 文件操作
cp -r dir1 dir2          # 复制目录
rm -rf dir               # 强制删除目录（谨慎使用）
find /path -name "*.txt" # 查找文件
grep "text" file         # 在文件中搜索文本

# 3. 系统信息
df -h                    # 磁盘使用情况
free -h                  # 内存使用情况
top                      # 实时系统监控
htop                     # 增强版系统监控（需安装）

# 4. 进程管理
ps aux | grep process    # 查找进程
kill -9 PID              # 强制结束进程
pkill firefox            # 按名称结束进程

# 5. 网络相关
ip addr                  # 查看 IP 地址
ping google.com          # 测试网络连接
netstat -tulpn           # 查看端口占用

# 6. 包管理
sudo apt update          # 更新软件列表
sudo apt upgrade         # 升级所有软件
sudo apt install package # 安装软件

# 7. 权限管理
chmod 755 script.sh      # 修改文件权限
sudo chown user:group file # 修改文件所有者

# 8. 压缩解压
tar -xzf file.tar.gz     # 解压 tar.gz
unzip file.zip           # 解压 zip

# 9. 系统服务
sudo systemctl status service   # 查看服务状态
sudo systemctl restart apache2  # 重启服务

# 10. 日志查看
journalctl -xe           # 查看系统日志
tail -f /var/log/syslog  # 实时查看日志
```



# Ubuntu Commonly Used Software

## Terminator
[[Terminator]]

## Docker
[[Docker]]

## Obsidian
[[Obsidian]]

## Gitkraken

```bash
# gitkraken
wget https://release.axocdn.com/linux/gitkraken-amd64.deb
sudo dpkg -i gitkraken-amd64.deb
```
# Nvidia Driver
1. 禁用自带驱动
```bash
sudo gedit /etc/modprobe.d/blacklist_nouveau.conf

blacklist nouveau
options nouveau modeset=0
```

2. 卸载显卡驱动
```bash
sudo apt-get --purge remove nvidia-*
```

3. 查看系统中驱动版本，选择推荐的驱动版本进行安装：如安装535版本驱动命令如下
```bash
ubuntu-drivers devices
sudo apt install nvidia-driver-535
```

4. 重启电脑
```bash
reboot
```

5. 验证
```bash
nvidia-smi
```

6. 存在问题
``` bash
# 更新驱动之后重启电脑显示PPM init failed(-110)
# 采用独显直连

# 更新驱动前调节亮度没有反映  
# 更新Nidia显卡驱动之后可调节亮度
```

## Reference
1. [【超详细】【ubunbu 22.04】 手把手教你安装nvidia驱动，有手就行，隔壁家的老太太都能安装_ubuntu安装nvidia显卡驱动-CSDN博客](https://blog.csdn.net/huiyoooo/article/details/128015155)
2. [[2025-03-20#一、Nidia显卡驱动(apt install)]]

# CUDA

## 以`deb`方式安装

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
## 以`run`方式安装

```bash
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run
sudo sh cuda_11.8.0_520.61.05_linux.run
```
## Reference
-  [[2025-03-20#二、CUDA(`run`文件安装)]]
-  [CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive)

# CUDNN

## 以`deb`方式安装

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

## 以`deb`方式安装
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