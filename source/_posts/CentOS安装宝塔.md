---
title: CentOS安装宝塔
top: false
cover: false
toc: true
mathjax: true
date: 2019-06-24 18:34:44
password: 199897
summary:
tags: [服务器,宝塔]
categories: 服务器
---

1.安装可视化面板
```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install.sh && sh install.sh
```
注意：代码没有换行！如出错，尝试在下面复制，或先复制到记事本删除换行再粘贴到终端。
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install.sh && sh install.sh

输入命令后，系统自动下载安装环境，然后输入 y 进行确认。 然后等待约1-5分钟
![](https://note.youdao.com/yws/public/resource/a7b28e89afc8e429d20c7293f6faa483/xmlnote/3FBD6FCD15154A6D8151658F4868B63E/4485)
如无意外，最后会出现如下类似内容

```
Bt-Panel: http://111.230.15.237:8888
username: *******
password: *******
Warning:
If you cannot access the panel,
release the following port (8888|888|80|443|20|21) in the security group
```
系统自动生成账号密码，
username 项为账号，
pwssword 为密码。
请保存好你的账号密码。

2.启动面板与管理

- 启动面板

控制面板支持：

一键配置服务器环境（ LAMP / LNMP ）

一键安全重启

一键创建管理网站、ftp、数据库

一键配置（定期备份、数据导入、伪静态、301、SSL、子目录、反向代理、切换 PHP 版本）

数据库一键导入导出

系统监控（ CPU、内存、磁盘IO、网络IO ）

防火墙端口放行

SSH 开启与关闭及 SSH 端口更改
...

请复制以下命令到终端 ,然后稍等

```
service bt restart
```

- 访问面板
控制面板地址端口为 8888 ，
你的控制面板地址为 http://123.207.230.231:8888

请复制链接到新窗口打开


- 添加站点

在控制面板中，点击左侧导航栏的 网站 一项，添加网站。 域名： 填你的ip 123.207.230.231
备注： test
根目录：/www/wwwroot/test
FTP 、 数据库 两项中，账号密码都填 test
点击 提交 即可