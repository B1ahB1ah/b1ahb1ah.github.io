---
title: 0x07_SSR+魔改BBR(Debian平台)
date: 2020-01-01 11:08:27
categories: shadowsocks
tags: 
	- SSR 
	- 魔改BBR
---

## 一、安装SSR

sudo -i

wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh

chmod +x shadowsocks-all.sh

./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log

apt-get -y install wget..(if need)



## 二、SSR相关维护命令

~~~
启动SSR：
/etc/init.d/shadowsocks-r start
退出SSR：
/etc/init.d/shadowsocks-r stop
重启SSR：
/etc/init.d/shadowsocks-r restart
SSR状态：
/etc/init.d/shadowsocks-r status
卸载SSR：
./shadowsocks-all.sh uninstall
~~~



## 三、安装魔改BBR

wget --no-check-certificate https://github.com/tcp-nanqinlang/general/releases/download/3.4.2.1/tcp_nanqinlang-fool-1.3.0.sh

bash tcp_nanqinlang-fool-1.3.0.sh

reboot

sudo -i

bash tcp_nanqinlang-fool-1.3.0.sh