---
title: Linux 搭建 LNMP 环境
top: false
cover: false
toc: true
mathjax: true
date: 2020-02-17 21:12:30
password:
summary:
tags: 服务器环境
categories:
---

本教程以 Ubuntu 16.04 操作系统为例讲解如何搭建 LNMP 环境。

1.在操作系统安装完毕后你需要更新下系统，执行
```
sudo apt-get update && sudo apt-get dist-upgrade
```


安装 screen

screen 可以创建一个后台会话，将任务放在后台执行，非常适合比如编译软件、编译内核、安装更新等任务。

1.安装
```
sudo apt-get install screen
```
2.创建一个会话
```
screen -S lnmp
```

下载 LNMP 安装包

可以[去这里](https://lnmp.org/download.html) 下载最新的 lnmp

安装包进行编译安装，或直接在命令行执行如下命令
```
wget -c http://soft.vpser.net/lnmp/lnmp1.4-full.tar.gz
tar zxvf lnmp1.4-full.tar.gz
cd lnmp1.4-full
./install
```

执行上面的命令后按照要求输入数据库密码、选择数据库的类型(提供 mysql 和 mariadb ) 以及 PHP 的版本即可进行编译安装。

```
root@centos:~/lnmp1.4-full# ./install.sh

+------------------------------------------------------------------------+
|          LNMP V1.4 for Ubuntu Linux Server, Written by Licess          |
+------------------------------------------------------------------------+
|        A tool to auto-compile & install LNMP/LNMPA/LAMP on Linux       |
+------------------------------------------------------------------------+
|           For more information please visit https://lnmp.org           |
+------------------------------------------------------------------------+
You have 5 options for your DataBase install.
1: Install MySQL 5.1.73
2: Install MySQL 5.5.56 (Default)
3: Install MySQL 5.6.36
4: Install MySQL 5.7.18
5: Install MariaDB 5.5.56
6: Install MariaDB 10.0.30
7: Install MariaDB 10.1.23
0: DO NOT Install MySQL/MariaDB
Enter your choice (1, 2, 3, 4, 5, 6, 7 or 0): 7 # 选择数据库，部分版本的数据库需要内存大于2G
You will install MariaDB 10.1.23
===========================
Please setup root password of MySQL.(Default password: root) # 设置mysql root 密码
Please enter: 123456@#
MySQL root password: 123456@#
===========================
Do you want to enable or disable the InnoDB Storage Engine? # 是否安装 InnoDB 引擎
Default enable,Enter your choice [Y/n]: y
You will enable the InnoDB Storage Engine
===========================
You have 6 options for your PHP install. # 选择 PHP 版本
1: Install PHP 5.2.17
2: Install PHP 5.3.29
3: Install PHP 5.4.45
4: Install PHP 5.5.38 (Default)
5: Install PHP 5.6.31
6: Install PHP 7.0.21
7: Install PHP 7.1.7
Enter your choice (1, 2, 3, 4, 5, 6 or 7): 7
You will install PHP 7.1.7
===========================
You have 3 options for your Memory Allocator install.
1: Don't install Memory Allocator. (Default)
2: Install Jemalloc
3: Install TCMalloc
Enter your choice (1, 2 or 3): 2
You will install JeMalloc

Press any key to install...or Press Ctrl+c to cancel # 按任意键继续安装
```

在安装过程中如果你开启了 screen 则可以关闭会话，编译大约需要30分钟左右，如希望查看安装进度，可以再次连接服务器，执行

```
screen -r lnmp
```

查看该会话。

安装完毕会提示类似如下的信息

```
State      Recv-Q Send-Q Local Address:Port               Peer Address:Port
LISTEN     0      128          *:80                       *:*
LISTEN     0      128          *:22                       *:*
LISTEN     0      128         :::22                      :::*
LISTEN     0      128         :::3306                    :::*
Install lnmp takes 59 minutes.
Install lnmp V1.4 completed! enjoy it.
```

程序会自动开放80 3306端口