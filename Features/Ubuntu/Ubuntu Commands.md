# 文件和目录操作
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
# 系统信息
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
# 软件包管理

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
# 用户和权限管理
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
# 进程管理
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
# 网络命令
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

# 系统服务管理
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

# 文件搜索
```bash
# 在文件系统中搜索文件
find / -name "filename"

# 在文件内容中搜索文本（-i 忽略大小写，-r 递归搜索目录）
grep -ir "keyword" /path/to/search
```

# 压缩与解压
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
# 其他常用命令
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

  

  

  