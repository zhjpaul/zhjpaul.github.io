---
layout: post
title:  "在Windows和Ubuntu中部署Samba"
date:   2017-06-01
tags:   [tool, windows, ubuntu, smaba]
---

## 部署Samba

参考[这篇文章](http://blog.163.com/baosongliang@126/blog/static/194935702013729112431894/)进行部署，只是觉得这篇文章排版不是很好，故而自己重新排版记录一下。

部署时以Ubuntu作为Samba服务器端，Windows作为客户端。其中Ubuntu版本为14.04，windows为windows7。

## Samba服务器端

#### 1. 关闭Linux防火墙，同时移除系统原有的Samba，重新进行Samba的安装；

```shell
sudo ufw disable
sudo apt-get remove samba-common
sudo apt-get install samba
```

#### 2. 修改配置文件`/etc/samba/smb.conf`，并在文件末尾添加如下内容；

```shell
[root]
    comment = rootdir
    browseable = yes
    writable = yes
    path = /
    valid users = smb
[share]
    comment = WHAT_YOUR_WANT_TO_SAY
    path = PATH_TO_YOUR_SHARE_DIRECTROY
    public = yes
    writable = yes
```

#### 3. 运行Samba服务。

```shell
sudo /etc/init.d/smbd start   # start smb service
sudo /etc/init.d/smbd restart # restart smb service
```

## Samba客户端

#### 1. 在Windows下访问共享目录；

```shell
# suppose ubuntu's IP is 192.168.1.123
\\192.168.1.123\share
```

如果Windows下不能对共享文件进行修改，可以执行`chmod -R go+rwx YOUR_SHARE_DIRECTORY`。

#### 2. 在Windows下添加网络驱动盘；

右键我的电脑->映射网络驱动器，然后在弹出的对话框中选择一个盘符，同时在**文件夹**中填入步骤1中访问的共享文件`\\192.168.1.123\share`。
