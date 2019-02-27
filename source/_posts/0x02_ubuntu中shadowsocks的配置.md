---
title:  0x02_ubuntu中shadowsocks配置
date: 2018-06-06 00:51:56
categories: shadowsocks
tags: 
	- shadowsocks
---

### 安装shadowsocks

首先你得有一个shadowsocks帐号,可以自己购买VPS搭建,也可购买,这里就不多叙述了.

安装shadowsocks

```
sudo apt-get install shadowsocks
```

设置shadowsocks.json配置文件我一般把他存在/home/user/tools/里,进入目录

```
sudo vim /home/user/tools/shadowsocks.json
```

<!-- more  -->

格式如下

```
{
        "server":"xx.xx.xx.xx",
        "server_port":9527,
        "local_address":"127.0.0.1",
        "local_port":1080,
        "password":"your_passwd",
        "timeout":300,
        "method":"aes-256-cfb"
}
```
接下来就可以用sslocal命令启动ss代理服务了.

但是每次开机都要手动输入太low了不是.



