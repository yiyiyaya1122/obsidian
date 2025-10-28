# Install

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

## Reference
- [Installing the NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)
- [[2025-10-28#`docker`安装]]

# Use

```bash
# ==================== Ubuntu 常用命令大全 ====================

# 1. 镜像操作
docker images # 列出本地镜像
docker search image_name # 搜索镜像（从 Docker Hub）
docker pull image_name:tag # 拉取镜像（从 Docker Hub）默认为 latest 标签
docker build -t my_image:1.0 .  # 构建镜像（-t 指定标签，. 表示使用当前目录的 Dockerfile）
docker rmi image_id/image_name -f # 删除本地镜像（-f 强制删除）
docker save -o image.tar image_name # 保存镜像为 tar 文件
docker load -i image.tar # 从 tar 文件加载镜像

# 2. 容器操作
docker run -d -p 8080:8080 -v /host/path:/container/path --name my_container image_name # 运行容器（-d 后台运行，-p 端口映射，-v 挂载卷）
docker ps # 列出运行中的容器
docker ps -a # 列出所有容器（包括已停止的）
docker stop container_id/name # 停止容器
docker start container_id/name # 启动容器
docker restart container_id/name # 重启容器
docker rm container_id/name -f # 删除容器（-f 强制删除运行中的容器）
docker logs -f -n 100 container_id/name # 查看容器日志（-f 跟踪日志输出，-n 显示最后 n 行）
docker exec -it container_id/name /bin/bash # 进入运行中的容器（-it 交互式终端）
docker stats container_id/name # 查看容器资源使用情况
docker cp /host/path container_id/name:/container/path # 复制文件/目录到容器
docker cp container_id/name:/container/path /host/path # 从容器复制文件/目录到主机

```

  