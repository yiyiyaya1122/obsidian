# 镜像操作
```bash
# 列出本地镜像
docker images

# 搜索镜像（从 Docker Hub）
docker search image_name

# 拉取镜像（从 Docker Hub）
docker pull image_name:tag  # 默认为 latest 标签

# 构建镜像（-t 指定标签，. 表示使用当前目录的 Dockerfile）
docker build -t my_image:1.0 .

# 删除本地镜像（-f 强制删除）
docker rmi image_id/image_name -f

# 保存镜像为 tar 文件
docker save -o image.tar image_name

# 从 tar 文件加载镜像
docker load -i image.tar
```

# 容器操作
```bash
# 运行容器（-d 后台运行，-p 端口映射，-v 挂载卷）
docker run -d -p 8080:8080 -v /host/path:/container/path --name my_container image_name

# 列出运行中的容器
docker ps

# 列出所有容器（包括已停止的）
docker ps -a

# 停止/启动/重启容器
docker stop container_id/name
docker start container_id/name
docker restart container_id/name

# 删除容器（-f 强制删除运行中的容器）
docker rm container_id/name -f

# 查看容器日志（-f 跟踪日志输出，-n 显示最后 n 行）
docker logs -f -n 100 container_id/name

# 进入运行中的容器（-it 交互式终端）
docker exec -it container_id/name /bin/bash

# 查看容器资源使用情况
docker stats container_id/name

# 复制文件/目录到容器
docker cp /host/path container_id/name:/container/path

# 从容器复制文件/目录到主机
docker cp container_id/name:/container/path /host/path
```

# 容器生命周期管理
```bash
# 暂停/恢复容器
docker pause container_id/name
docker unpause container_id/name

# 查看容器详细信息
docker inspect container_id/name

# 查看容器进程
docker top container_id/name
```

# 网络操作
```bash
# 列出网络
docker network ls

# 创建网络（-d 指定驱动类型）
docker network create -d bridge my_network

# 连接容器到网络
docker network connect my_network container_id/name

# 断开容器与网络的连接
docker network disconnect my_network container_id/name

# 删除网络
docker network rm my_network
```

# 卷操作
```bash
# 列出卷
docker volume ls

# 创建卷
docker volume create my_volume

# 删除卷
docker volume rm my_volume

# 查看卷详细信息
docker volume inspect my_volume

# 清理未使用的卷
docker volume prune
```

# Docker Compose 命令（需先安装）
```bash
# 根据 docker-compose.yml 启动服务（-d 后台运行）
docker-compose up -d

# 停止并删除服务
docker-compose down

# 查看服务状态
docker-compose ps

# 构建或重建服务
docker-compose build

# 查看服务日志
docker-compose logs -f service_name
```

# 系统命令
```bash
# 查看 Docker 系统信息
docker info

# 清理所有未使用的容器、网络、卷和镜像
docker system prune -a

# 查看磁盘使用情况
docker system df
```

# 镜像仓库操作

```bash
# 登录到 Docker 镜像仓库
docker login registry.example.com

# 为镜像添加标签（准备推送）
docker tag local_image:tag registry.example.com/repo/image:tag

# 推送镜像到仓库
docker push registry.example.com/repo/image:tag

# 从仓库拉取镜像
docker pull registry.example.com/repo/image:tag
```
  

  

  