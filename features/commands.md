
# Ubuntu

## 文件和目录操作
```bash
# 列出目录内容（-l 长格式，-a 显示隐藏文件，-h 以人类可读格式显示大小）
ls -lah

# 切换目录（进入指定目录）
cd /path/to/directory

# 创建目录（-p 递归创建父目录）
mkdir -p new_directory/subdirectory

# 删除文件或目录（-r 递归删除目录，-f 强制删除不提示）
rm -rf file.txt directory

# 复制文件或目录（-r 递归复制目录）
cp -r source/ destination/

# 移动文件或目录（也可用于重命名）
mv old_name new_name

# 查看文件内容（-n 显示行号）
cat -n file.txt

# 查看文件前几行/后几行
head file.txt
tail -f log.txt  # -f 实时跟踪文件更新

# 编辑文件（使用 nano 编辑器，也可用 vim、gedit 等）
nano file.txt
```
## 系统信息
```bash
# 显示当前系统信息（内核版本、系统名称等）
uname -a

# 查看系统发行版信息
lsb_release -a

# 查看磁盘使用情况（-h 以人类可读格式显示）
df -h

# 查看内存使用情况
free -h

# 查看 CPU 信息
lscpu

# 查看网络连接（-t 显示 TCP 连接，-u 显示 UDP 连接）
netstat -tupln
```
## 软件包管理

```bash
# 更新可用软件包列表
sudo apt update

# 升级已安装的软件包
sudo apt upgrade

# 安装软件包
sudo apt install package_name

# 移除软件包（--purge 同时删除配置文件）
sudo apt remove --purge package_name

# 搜索软件包
apt search keyword

# 清理不再需要的依赖和缓存
sudo apt autoremove
sudo apt clean
```
## 用户和权限管理
```bash
# 创建新用户（-m 创建主目录）
sudo adduser new_user

# 删除用户（-r 同时删除主目录）
sudo deluser -r existing_user

# 添加用户到组（例如 sudo 组）
sudo usermod -aG sudo username

# 更改文件权限（r=读 4，w=写 2，x=执行 1）
chmod 755 script.sh  # 所有者有所有权限，组和其他用户有读和执行权限

# 更改文件所有者和组
chown user:group file.txt
```
## 进程管理
```bash
# 查看正在运行的进程
ps aux

# 查看实时进程活动
top

# 终止进程（-9 强制终止）
kill -9 process_id

# 后台运行命令（使用 &）
nohup command &  # nohup 防止进程在会话结束时终止
```
## 网络命令
```bash
# 查看 IP 地址（也可用 ifconfig，但需要安装 net-tools）
ip addr show

# 测试网络连接
ping google.com

# 追踪网络数据包路径
traceroute google.com

# 显示路由表
route -n

# 下载文件（-O 指定输出文件名）
wget -O output.zip https://example.com/file.zip

# 传输文件（需要 openssh-client 包）
scp user@remote:/path/to/file .
```

## 系统服务管理
```bash
# 启动/停止/重启服务
sudo systemctl start service_name
sudo systemctl stop service_name
sudo systemctl restart service_name

# 查看服务状态
sudo systemctl status service_name

# 设置服务开机自启/禁用
sudo systemctl enable service_name
sudo systemctl disable service_name
```

## 文件搜索
```bash
# 在文件系统中搜索文件
find / -name "filename"

# 在文件内容中搜索文本（-i 忽略大小写，-r 递归搜索目录）
grep -ir "keyword" /path/to/search
```

## 压缩与解压
```bash
# 创建 tar 压缩包
tar -cvf archive.tar files/

# 创建 tar.gz 压缩包（-z 使用 gzip 压缩）
tar -czvf archive.tar.gz files/

# 解压 tar.gz 文件
tar -xzvf archive.tar.gz

# 解压 zip 文件
unzip file.zip
```
## 其他常用命令
```bash
# 查看命令帮助信息
command --help
man command  # 查看命令手册

# 显示当前日期和时间
date

# 显示当前用户
whoami

# 关机/重启（立即执行）
sudo shutdown -h now
sudo reboot
```

  
# Docker

## 镜像操作
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

## 容器操作
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

## 容器生命周期管理
```bash
# 暂停/恢复容器
docker pause container_id/name
docker unpause container_id/name

# 查看容器详细信息
docker inspect container_id/name

# 查看容器进程
docker top container_id/name
```

## 网络操作
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

## 卷操作
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

## Docker Compose 命令（需先安装）
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

## 系统命令
```bash
# 查看 Docker 系统信息
docker info

# 清理所有未使用的容器、网络、卷和镜像
docker system prune -a

# 查看磁盘使用情况
docker system df
```

## 镜像仓库操作

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
  

  

  