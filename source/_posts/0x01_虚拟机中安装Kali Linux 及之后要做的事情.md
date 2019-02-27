---
title: 0x01.虚拟机中安装Kali Linux 及之后要做的事情
date: 2018-05-28 00:51:56
categories: Linux
tags: 
	- Kali
---



## 1. 参考文献

[Kali 安装详细步骤](https://blog.csdn.net/u012318074/article/details/71601382/)

[安装 Kali Linux 2018.1 及之后的事](https://blog.csdn.net/metaphorxi/article/details/79639862)

---
---

## 2. Kali Linux 在虚拟机中的安装

<!-- more -->

### 镜像下载

镜像源文件在清华资源站下载，使用VMware Workstation 12安装。

### 创建普通用户

一开始默认用root账户登录,一不小心就作了大死把bin目录全删了,重装了几次
血泪教训,还是保险点用普通用户+sudo吧
```
#创建用户
useradd username -p password 
#删除用户
userdel username

```


### 更换国内源

然后进行更换国内源，建议使用阿里云源：

首先打开 sources.list
```
vim /etc/apt/sources.list
```
然后添加源（阿里云的源就够用啦）
```
#阿里云
deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib

#中科大
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib

#浙大
deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free

#清华大学
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free

#官方源
deb http://http.kali.org/kali kali-rolling main non-free contrib
deb-src http://http.kali.org/kali kali-rolling main non-free contrib
```

### 安装VMware Tools

依次选择“虚拟机” --“安装VMware Tools”

加载完成后，复制VMware Tools-10.0.10***.tar.gz （不同版本具体名字不同）到 home 目录 tools 文件夹（tools文件夹需要手动创建），
解压：
```
tar -xzvf VMware Tools ***.tar.gz，VMware Tools ***.tar.gz
```
根据自己文件内容要换成具体的文件名。
进入vmware-tools-distrib后执行
```
./vmware-install.pl
```
如果第一次询问是否安装，输入yes，之后一路回车即可，
看到Enjoy，--the WMware team即表示安装完成
重启后选择“进入全屏模式”，能进入全屏模式说明增强工具已经安装成功。


### 更新系统数字签名
```
wget -q -O - https://archive.kali.org/archive-key.asc | apt-key add
```
很重要,很重要,真的很重要!!!
重要的事情说三遍,没有这一步t-get根本用不了


### 更新软件包

依次执行下面三行代码,根据网速大概要15-20分钟
```
sudo apt-get update#更新软件
sudo apt-get upgrade
sudo apt-get dist-upgrade #升级系统
```
<br />

---

---

## 3. Kali安装后的用户体验提升

### 安装中文输入法

由于Kali不自带中文输入法,所以,你懂得,自己动手风衣足食

下载搜狗输入法linux版：[搜狗输入法linux版](http://pinyin.sogou.com/linux/?r=pinyin)
选择 64 位版本 
确认下载完成后进入安装环节。

输入法需要用到 fcitx，所以需要先安装
```
apt-get install fcitx fcitx-config-gtk2
```

进入到“下载”目录中（可以使用复制粘贴），执行
```
dpkg -i sogoupinyin_2.1.0.0082_amd64.deb
```

如果出现报依赖问题，根据提示输入
```
apt-get install -f
```
重新执行
```
dpkg -i sogoupinyin_2.1.0.0082_amd64.deb
```
重启后，使用shift键切换中英文输入法即可 


### 安装谷歌chrome浏览器

这里我选择不使用自带的firefox浏览器,二者都是开源浏览器
但是有谷歌帐号的话用户体验差别不是一般的大啊,用过的肯定都知道: )
chrome登录后会自动同步书签,插件设置,主题设置,真正一键搞定啊有没有
大佬就是大佬,不像火狐"科学上网"安个插件都卡半天
废话不多说,开搞~

根据自己系统时32位或64位选择安装包,不过现在一般都是64位了吧
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```

cd进入下载目录
```
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

Enjoy Chrome
要打开Google Chrome，请点击Unity Launcher顶部的“破折号”按钮，然后输入“Google Chrome”。与短语匹配的项目开始显示在搜索框下方。当显示“Google Chrome”项目时，点击它可启动Chrome。
如果有谷歌帐号,在下面翻墙后就可以很方便了.


### Kali翻墙-----shadowsocks+proxychains+chrome-switchyomega插件

首先你得有一个shadowsocks帐号,可以自己购买VPS搭建,也可购买,这里就不多叙述了.

安装shadowsocks
```
sudo apt-get install shadowsocks
```
设置shadowsocks.json配置文件
我一般把他存在/home/user/tools/里,进入目录
```
sudo vim /home/user/tools/shadowsocks.json
```
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
启用本地ss服务
```
#后台启动-d start本地服务
sudo sslocal -c /home/user/tools/shadowsocks.json -d start
```

利用proxychains暂时科学上网下载chrome插件
为什么要用proxychains呢?
因为要开启chrome代理,先要下载switchyomega插件,而要下载此插件,需要翻墙...
相当于switchyomega是chrome自带的代理插件,我们要先借助别的插件翻墙来安装chrome的插件
但proxychains只能分应用代理
面倒的丝..所以proxychains只做过渡用,
```
#安装
sudo apt-get install proxychains
```

配置proxychains
```
sudo vim /etc/proxychains.conf
```

注释其最下面一行
```
socks4 127.0.0.1 1080
```

并添加一行
```
socks5 127.0.0.1 1080
#注意!! 这里的地址要和你shadowsocks.json里的local_address与local_port一致
```

proxychains使用
格式: proxychains + 应用名
```
proxychains google-chrome
```
此时打开的chrome浏览器就可以科学上网了

安装配置switchomega插件
打开chrome网上商店-搜索'swithyomega'-添加到chrome
在浏览器右上角会出现一个圆圈
右击圆圈--'选项'--在'proxy'选项中填入socks5代理(和proxychains配置一致)

之后配置"autoproxy"情景:

![xxxxxx](/images/autoproxy.jpg)

其中"规则列表网址"为

```
https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt
```

完成后别忘了左边"应用选项",最后关闭此页面 在右上角圆圈选择"autoproxy"

done!

