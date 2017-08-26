---
layout: post
title:  "Ubuntu 14.04下常见问题记录"
tags:   [ubuntu]
date:   2017-05-07
---

### Q001: [Error] sudo apt-get install xxx

**Description**

```shell
E: Could not get lock /var/lib/dpkg/lock - open (11:Resource temporarily unavaliable)
E: Unable to lock the administration directory (/var/lib/dpkg/), is another process using it? 
```
 
**Solution**

```shell
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpgk/lock
```

### Q002: [Error] ping: unknown host xx.xx.xx.xx

**Description**

```shell
ping www.baidu.com
=> ping: unknown host www.baidu.com
```

**Solution**

1. 首先ping一下ip地址，譬如`ping 8.8.8.8`，如果可以ping通的话转2，否则转3；
2. 转到此处说明是DNS解析问题，可以查看配置文件`/etc/resolv.conf`，可以通过`nameserver xx.xx.xx.xx`的方式添加DNS服务器；
3. 转到此处说明是网络配置问题，首先查看是否有内网地址，如果没有的话首先配置ip地址，否则直接进行默认网关的配置。

```shell
# ip地址的配置 (以192.168.1.1/24为例)
sudo ifconfig eth0 192.168.1.202/24

# 默认网关的配置
sudo route add default gw 192.168.1.1
```

### Q003: [Error] Python <MARKER_EXPR>

**Description**

我在安装IPython之后运行IPython的过程中出现了这个错误，错误信息如下：

```shell
MARKER_EXPR = originalTextFor(MARKER_EXPR())("marker")
TypeError: __call__() takes exactly 2 arguments (1 given)
```

**Solution**

网上提到了的解决方法基本上大同小异，常见的解决方案如下：

```shell
sudo pip install --upgrade --force pip  # update pip to 1.5.4 to 9.0.1
sudo pip install setuptools 
```

但是这个方案并没有解决我出现的问题，然后参考了[这篇博客](http://blog.csdn.net/shanexia/article/details/55006571)，又进行了如入修改，问题得到了解决。其中MARKER_EXPR所在的文件可以参考错误信息。

```shell
# MARKER_EXPR = originTextFor(MARKER_EXPR())("marker")
MAKRER_EXPR = originTextFor(MARKER_EXPR)("marker")
```

### Q004: [Error] dpkg: error processing package xxx

**Description**

```shell
dpkg: error processing package erlang-mode ...
```

**Solution**

```shell
sudo mv /var/lib/dpkg/info/ /var/lib/dpkg/info_old/
sudo mkdir /var/lib/dpkg/info/
sudo apt-get update
sudo apt-get -f install
sudo mv /var/lib/dpkg/info/* /var/lib/dpkg/info_old/
sudo rm -rf /var/lib/dpgk/info
sudo mv /var/lib/dpkg/info_old/ /var/lib/dpgk/info/
```
