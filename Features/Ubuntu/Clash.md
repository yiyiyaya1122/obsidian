# Install

```bash

# 1.下载clash
# https://gitee.com/mgod_wu/clash-for-all-backup/releases/tag/v0.20.39

# 2.解压clash
tar zxvf Clash.for.Windows-0.20.39-x64-linux.tar.gz

# 3.移动到opt
sudo mv Clash\ for\ Windows-0.20.39-x64-linux /opt/clash
cd /opt/clash  
./cfw
```


# Issue

>[! ERROR]
 > **could not connect to clash core, logs are not available.**

![[Pasted image 20251114143205.png]]

```bash
# 进入 Clash 目录
cd /opt/clash
# 给整个目录添加适当的权限
sudo chmod -R 755 /opt/clash
sudo chown -R $USER:$USER /opt/clash

# 特别确保核心文件有执行权限
sudo chmod +x cfw

```

![[Pasted image 20251114180557.png]]
# Use
详见`Reference`




## Reference
- [Linux/Ubuntu 安装图形界面版 clash-gui](https://www.mgodmonkey.cn/posts/a5d6f412.html
- [Ubuntu 使用 Clash For Linux 客户端教程](https://doc.6bc.net/article/35/)