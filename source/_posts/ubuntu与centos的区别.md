---
title: ubuntu与centos的区别
top: false
cover: false
toc: true
mathjax: true
date: 2018-03-16 15:43:54
password:
summary:
tags: [Linux,ubuntu,centos]
categories: Linux
---

# ubuntu与centos的区别 #
**共同点**

1.两个系统都分别有桌面系统与服务器系统，不过ubuntu的桌面从外观上来看要比centos的漂亮 
![](https://i.imgur.com/wG2Wijz.png)

**不同点**

1.centos中新建的普通用户是没有sudo权限的，如果想让普通用户拥有sudo权限需要在/etc/sudoers文件中添加用户的权限，而ubuntu系统普通用户想要使用sudo权限  直接使用sudo +命令行的方式就可以了
![](https://i.imgur.com/F9j1bQf.png)
![](https://i.imgur.com/gO8IHXy.png)

2.安装软件包命令格式不一样。centos使用yum的方式，而Ubuntu使用apt-get 方式。
![](https://i.imgur.com/5HVsSwb.png)

3.由于centos是基于redhat的，所以centos支持rpm包，但Ubuntu不支持。
![](https://i.imgur.com/ncFb1r6.png)

4.现在虽然说ubuntu系统也可以使用服务器端来进行使用了，但相对centos来说并没有centos稳定。而且在一些比较知名的技术论坛大多都是关于centos的，所以在遇到问题查询资料的时候相对要比ubuntu要更方便一些。如下图中centos中文站技术论坛，是很多学习者经常查询问题的地方。
![](https://i.imgur.com/dZWrs2n.png)