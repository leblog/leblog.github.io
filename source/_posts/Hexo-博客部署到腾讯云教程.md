---
title: Hexo 博客部署到腾讯云教程
top: false
cover: false
toc: true
mathjax: true
date: 2018-07-03 18:33:42
password:
summary:
tags: [教程,学习笔记]
categories: 教程
---


>- 本文首发于我的个人博客：[乐乐的博客](leblog.github.io)
> - 文章链接：[传送门]()

 >本篇内容用来讲述如何将 hexo 博客部署到腾讯云的服务器上。
只要通过三步即可成功部署：
>- 云服务器端 git 的配置
>- Nginx 的配置
>- 本地端 hexo 的设置更改

下面开始正式讲解如何部署。

**前期需要准备**：

- 一个腾讯云服务器
- hexo 本地博客

顺便说下我的服务器环境：
| 操作系统            | CPU | 内存  | 带宽    |
|-----------------|-----|-----|-------|
| CentOS 7\.2 64位 | 1核  | 2GB | 1Mbps |

# 1. 进入云服务器中
- 首先点击下边网站，登录你的进入云服务器的控制台
腾讯云服务器的控制台：https://console.cloud.tencent.com/cvm/index

![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/864802B7DBE0495F912DBFCD76517FFE/1290)

-  左边菜单选择云主机，然后找到你的服务器。点击登录
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/8C43CC8C4D3D456F96D1C0FC5704994E/1291)
-  输入密码，进入 云服务器 CentOS中。（初始密码在控制台右上角的消息列表中）
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/19E9FE5BE3B647C7AB13DA3559D22D24/1289)

# 2. 云服务器端配置 git

1.安装依赖库和编译工具

-  安装依赖库：
> yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel 

-  安装编译工具：
> yum install gcc perl-ExtUtils-MakeMaker package

2.下载git

- 选择一个目录来存放下载下来的git安装包。这里选择了``/usr/local/src``目录
    
>  cd /usr/local/src

- 到官网找一个新版稳定的源码包下载到 ``/usr/local/src`` 文件夹里
    
> wget https://www.kernel.org/pub/software/scm/git/git-2.16.2.tar.gz

- 解压编译 git

- 在当前目录下解压 ``git-2.16.2.tar.gz``

> tar -zvxf git-2.16.2.tar.gz

- 进入 git-2.16.2.tar.gz 目录下

> cd git-2.16.2

- 执行编译

> make all prefix=/usr/local/git

- 安装 git 到 ``/usr/local/git`` 目录下

>make install prefix=/usr/local/git

4.配置 git 环境变量

- 将 git 加入 PATH 目录中

> echo 'export PATH=$PATH:/usr/local/git/bin' >> /etc/bashrc

- 使 git 环境变量生效

> source /etc/bashrc
 
5.查看 git 版本
>git --version

如果此时能查看到 git 的版本号，说明我们已经安装成功了。

6.创建 git 仓库，用于存放博客网站资源。

- 在 ``home/git`` 的目录下，创建一个名为``hexoBlog``的裸仓库（bare repo）。
如果没有 ``home/git`` 目录，需要先创建；然后修改目录的所有权和用户权限。

> mkdir /home/git/<br>
> chown -R $USER:$USER /home/git/<br>
> chmod -R 755 /home/git/

然后，执行如下命令：

>cd /home/git/<br>
>git init --bare hexoBlog.git

刚才这一步主要创建一个裸的 git 仓库。

7.创建一个新的 git 钩子，用于自动部署。

- 在 ``/home/git/hexoBlog.git`` 下，有一个自动生成的`` hooks`` 文件夹。我们需要在里边新建一个新的钩子文件 ``post-receive``。

> vim /home/git/hexoBlog.git/hooks/post-receive

按 `` i ``键进入文件的编辑模式，在该文件中添加两行代码（将下边的代码粘贴进去)，指定 Git 的工作树（源代码）和 Git 目录（配置文件等）。

>#!/bin/bash<br>
git --work-tree=/home/hexoBlog --git-dir=/home/git/hexoBlog.git checkout -f

然后，按`` Esc ``键退出编辑模式，输入``:wq ``保存退出。
修改文件权限，使得其可执行。
> chmod +x /home/git/hexoBlog.git/hooks/post-receive

到这里，我们的 git 仓库算是完全搭建好了。下面进行 Nginx 的配置。

# 3.云服务器端配置 Nginx

安装 Nginx
yum install -y nginx
启动 Nginx
service nginx start
测试 Nginx 服务器
wget http://127.0.0.1
能够正常获取以下欢迎页面说明Nginx安装成功。

```
Connecting to 127.0.0.1:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 43704 (43K) [text/html]
Saving to: ‘index.html’

100%[=======================================>] 43,704      --.-K/s   in 0s

2018-03-09 23:04:09 (487 MB/s) - ‘index.html’ saved [43704/43704]
```


- 测试网页是否能打开
在浏览器中输入服务器 ip 地址，就是服务器的公网 ip。

- 配置 Nginx 托管文件目录

    - 接下来，创建 ``/home/hexoBlog``目录，用于 ``Nginx`` 托管。
    >mkdir /home/hexoBlog/<br>
    chown -R $USER:$USER /home/hexoBlog/<br>
    chmod -R 755 /home/hexoBlog/
    
- 查看 Nginx 的默认配置的安装位置

> nginx -t

- 修改Nginx的默认配置，其中 cd 后边就是刚才查到的安装位置（每个人可能都不一样）

> vim /etc/nginx/nginx.conf

- 按方向键，找到如下位置

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    root /home/hexoBlog;    #需要修改
    
    server_name www.bujige.net; #需要修改
    
    # Load configuration files for the default server block.
    include /etc/nginx/default.d/*.conf;
    location / {
    }
    error_page 404 /404.html;
        location = /40x.html {
    }
```

按``i``键进入插入模式，将其中的 root 值改为`` /home/hexoBlog`` （刚才创建的托管仓库目录）。
将 server_name 值改成你的域名。

- 重启 Nginx 服务

>service nginx restart

至此，服务器端配置就结束了。接下来，就剩下本地 hexo 的配置更改了。

# 4. 修改 hexo 站点配置文件 git 相关设置

- 打开你本地的 hexo 博客所在文件，打开站点配置文件（不是主题配置文件），做以下修改。

>deploy:<br>
    type: git<br>
    repo: root@CVM 你的云服务器的IP地址:/home/git/hexoBlog<br>
    branch: master
    
- 在 hexo 目录下执行部署，试试看。

> cd 你的 hexo 目录<br>
hexo clean<br>
hexo generate<br>
hexo deploy<br>

- 打开你的公网 IP，看是不是已经部署成功了。
![](https://note.youdao.com/yws/public/resource/4446b015d9dc2fb92d362fab8b947642/xmlnote/BD3DBBB4EC2E49ABA90A87DE1E9C7875/1416)

- 最后一步，更改域名解析。这一步不再做介绍。
