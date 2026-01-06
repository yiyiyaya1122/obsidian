#  一、下载

访问如下网址，选择合适的版本下载，Ubuntu系统选择Clash.for.Windows-0.20.39-x64-linux.tar.gz即可。

```bash
https://github.com/MGod-monkey/clash-for-all-backup/releases
```

![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")
![](https://i-blog.csdnimg.cn/direct/f9409aa9e65b4fa28c170ddaf8d1dc26.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

# 二、安装

将上一步下载的Clash.for.Windows-0.20.39-x64-linux.tar.gz进行**解压**、**重命名**、**移动**。

```bash
# 1. 解压
tar zxvf Clash.for.Windows-0.20.39-x64-linux.tar.gz

# 2. 将解压后的Clash for Windows-0.20.39-x64-linux文件夹移动到opt文件夹下并重命名为clash
sudo mv Clash\ for\ Windows-0.20.39-x64-linux /opt/clash

```

![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")

# 三、使用

1. 运行如下命令，可打开clash界面，打开后界面如下图：

```bash
cd /opt/clash
./cfw
```

![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")

![](https://i-blog.csdnimg.cn/direct/e8eb668bf34749babd52c21b41cf0369.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")

2. 代理地址的导入只需要切换到 Profiles 页面，输入自己购买的订阅地址即可：

![](https://i-blog.csdnimg.cn/direct/3dd6484cecd3493cacd06bb6293d48e2.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

3. 成功订阅后，即可选择代理：

![](https://i-blog.csdnimg.cn/direct/7fa897667ab74af8ae687191512d8030.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

4. 注意，上述操作完成之后仍需**手动设置**网络代理才可科学上网，设置方法如下图：

![](https://i-blog.csdnimg.cn/direct/c2f5f7c0d88545c684e31b952464e235.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

![[Pasted image 20251114180557.png]]

# 四、进阶操作

Clash.for.Windows-0.20.39-x64-linux版本默认是没有桌面图标的，我们可以**手动配置桌面图标**。

```bash
# 切换到用户专属的桌面快捷方式配置目录（所有用户的桌面文件默认存放在此）
cd ~/.local/share/applications

# 使用 nano 编辑器创建并编辑名为 clash_gui.desktop 的桌面配置文件
nano clash_gui.desktop

# ==================== 以下是 nano 编辑器内需要输入的内容 ====================
[Desktop Entry]          # 固定格式，标识这是 Linux 桌面入口配置文件
Name=clash for linux     # 快捷方式显示的名称（桌面/应用列表中看到的名字）
Icon=/opt/clash/clash.png # 快捷方式的图标路径（需确保该图片文件存在）
Exec=/opt/clash/cfw      # 点击快捷方式时执行的程序路径（Clash GUI 的启动程序）
Type=Application         # 类型为应用程序（固定值，标识这是可执行程序的快捷方式）
# ==================== nano 编辑器内容结束 ====================

# 为该桌面配置文件添加可执行权限（Linux 要求桌面文件有执行权限才能生效）
sudo chmod a+x clash_gui.desktop
```

![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")

运行成功之后，即可在应用程序中看到 clash 的桌面图标：

![](https://i-blog.csdnimg.cn/direct/eb06171bbef346a295796ab58ea6a1e8.png)![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")​

# 五、其他

看很多同事在用clash-verge，此处贴出网址，有时间再补充。

```bash
https://github.com/clash-verge-rev/clash-verge-rev
```

![](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw== "点击并拖拽以移动")

# 六、常见问题

## 问题1

**问题现象：**

![[Pasted image 20251114143205.png]]

**解决方法：**

```bash
# 进入 Clash 目录
cd /opt/clash

# 给整个目录添加适当的权限
sudo chmod -R 755 /opt/clash
sudo chown -R $USER:$USER /opt/clash

# 特别确保核心文件有执行权限
sudo chmod +x cfw
```



# 七、参考

- [Linux/Ubuntu 安装图形界面版 clash-gui](https://www.mgodmonkey.cn/posts/a5d6f412.html "Linux/Ubuntu 安装图形界面版 clash-gui")
- [Ubuntu 使用 Clash For Linux 客户端教程](https://doc.6bc.net/article/35/ "Ubuntu 使用 Clash For Linux 客户端教程")

  

​