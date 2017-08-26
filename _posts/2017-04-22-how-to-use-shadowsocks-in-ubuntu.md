---
layout: post 
title:  "如何在Ubuntu 14.04中使用Shadowsocks客户端"
tags:   [tool, shadowsocks, ubuntu]
date:   2017-04-22
---



## 安装shadowsocks

- `sudo apt-get install python-gevent python-pip`
- `sudo pip install shadowsocks`
- `sudo apt-get install python-m2crypto`

## 配置shadowsocks服务器

创建一个`json`文件用于填写服务器，以下为一个示例。

```json
{
  "server": "xx.xx.xx.xx",
  "server_port": 8388,
  "local_port": 1080,
  "password": "xxxxxx",
  "timeout": 600,
  "method": "xxxxx"
}
```

## 启动

`sudo sslocal -c YOUR_CONFIG_FILE`
