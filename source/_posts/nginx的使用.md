---
title: nginx的使用
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-12 17:15:16
password:
summary:
tags: Nginx
categories:
---
![](http://nginx.org/nginx.png)
### 1.Nginx是什么？


1.1 nginx是一款高性能的http服务器/反向代理服务器一家电子邮件的（IMAP/POP3）代理服务器。有实验表明Nginx能够支持5W条链接的并发，并且对CPU,内存等资源消耗非常低，运行非常稳定，基本不用重启。

### 2.Nginx的下载

进入http://nginx.org/en/download.html 下载nginx
![img](https://s1.ax1x.com/2020/06/13/tvywCj.png)

### 3.Nginx安装
##### 3.1 nginx安装环境

nginx是C语言开发，建议在linux上运行.

**gcc**

安装nginx需要先将官网下载的源码进行编译，编译依赖gcc环境，如果没有gcc环境，需要安装gcc：``yum –y install gcc-c++``

 

**PCRE**

PCRE(Perl Compatible Regular Expressions)是一个Perl库，包括 perl 兼容的正则表达式库。nginx的http模块使用pcre来解析正则表达式，所以需要在linux上安装pcre库。

``yum install -y pcre pcre-devel``

注：pcre-devel是使用pcre开发的一个二次开发库。nginx也需要此库。

 

**zlib**

zlib库提供了很多种压缩和解压缩的方式，nginx使用zlib对http包的内容进行gzip，所以需要在linux上安装zlib库。

``yum install -y zlib zlib-devel``

 

**openssl**

OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及SSL协议，并提供丰富的应用程序供测试或其它目的使用。

nginx不仅支持http协议，还支持https（即在ssl协议上传输http），所以需要在linux安装openssl库。

``yum install -y openssl openssl-devel``

##### 3.2 编译安装
将nginx-1.8.0.tar.gz拷贝至linux服务器。

 

解压：

``tar -zxvf nginx-1.8.0.tar.gz``

``cd nginx-1.8.0``

 1、 configure

./configure --help查询详细参数（参考本教程附录部分：nginx编译参数）

 

参数设置如下：

        ./configure \
        
        --prefix=/usr/local/nginx \
        
        --pid-path=/var/run/nginx/nginx.pid \
        
        --lock-path=/var/lock/nginx.lock \
        
        --error-log-path=/var/log/nginx/error.log \
        
        --http-log-path=/var/log/nginx/access.log \
        
        --with-http_gzip_static_module \
        
        --http-client-body-temp-path=/var/temp/nginx/client \
        
        --http-proxy-temp-path=/var/temp/nginx/proxy \
        
        --http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
        
        --http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
        
        --http-scgi-temp-path=/var/temp/nginx/scgi

 

注意：上边将临时文件目录指定为/var/temp/nginx，需要在/var下创建temp及nginx目录

``mkdir -p /var/temp/nginx``

 

2、 编译安装

make

``make  install``

安装成功查看安装目录

##### 3.3 启动nginx

cd /usr/local/nginx/sbin/

./nginx 

 

查询nginx进程：



 

15098是nginx主进程的进程id，15099是nginx工作进程的进程id

 

注意：

执行./nginx启动nginx，这里可以-c指定加载的nginx配置文件，如下：

./nginx -c /usr/local/nginx/conf/nginx.conf

如果不指定-c，nginx在启动时默认加载conf/nginx.conf文件，此文件的地址也可以在编译安装nginx时指定./configure的参数（--conf-path= 指向配置文件（nginx.conf））


##### 3.4 停止nginx
方式1，快速停止：

``cd /usr/local/nginx/sbin``

``./nginx -s stop``

此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程。

 

方式2，完整停止(建议使用)：

``cd /usr/local/nginx/sbin``

``./nginx -s quit``

此方式停止步骤是待nginx进程处理任务完毕进行停止。

 

##### 3.5 重启nginx
方式1，先停止再启动（建议使用）：

对nginx进行重启相当于先停止nginx再启动nginx，即先执行停止命令再执行启动命令。

如下：

``./nginx -s quit``

``./nginx``

 

方式2，重新加载配置文件：

当nginx的配置文件nginx.conf修改后，要想让配置生效需要重启nginx，使用-s reload不用先停止nginx再启动nginx即可将配置信息在nginx中生效，如下：

``./nginx -s reload``

### 4.反向代理服务器

##### 4.1什么是反向代理
通常的代理服务器，只用于代理内部网络对Internet的连接请求，客户机必须指定代理服务器,并将本来要直接发送到Web服务器上的http请求发送到代理服务器中由代理服务器向Internet上的web服务器发起请求，最终达到客户机上网的目的。

而反向代理（Reverse Proxy）方式是指以代理服务器来接受internet上的连接请求，然后将请求转发给内部网络上的服务器，并将从服务器上得到的结果返回给internet上请求连接的客户端，此时代理服务器对外就表现为一个反向代理服务器。

如下图：![](https://s1.ax1x.com/2020/06/13/tvhSfO.jpg)

##### 4.2 nginx+tomcat反向代理

两个tomcat服务通过nginx反向代理，本例子使用三台虚拟机进行测试，

nginx服务器：192.168.101.3

tomcat1服务器：192.168.101.5

tomcat2服务器：192.168.101.6

如下图：
![](https://s1.ax1x.com/2020/06/13/tvh9pD.png)

##### 4.3 启动tomcat
tomcat使用apache-tomcat-7.0.57版本，在192.168.101.5和192.168.101.6虚拟机上启动tomcat。

 

##### 4.4 nginx反向代理配置
根据上边的需求在nginx.conf文件中配置反向代理，如下：

 

配置一个代理即tomcat1服务器

upstream tomcat_server1 {

            server 192.168.101.5:8080;

        }

配置一个代理即tomcat2服务器

    upstream tomcat_server2 {

            server 192.168.101.6:8080;

        }

 

配置一个虚拟主机

    server {

        listen 80;

        server_name aaa.test.com;

        location / {

域名aaa.test.com的请求全部转发到tomcat_server1即tomcat1服务上

                proxy_pass http://tomcat_server1;

欢迎页面，按照从左到右的顺序查找页面

                index index.jsp index.html index.htm;

        }

 

    }

 

    server {

        listen 80;

        server_name bbb.test.com;

 

        location / {

 域名bbb.test.com的请求全部转发到tomcat_server2即tomcat2服务上

                  proxy_pass http://tomcat_server2;

                  index index.jsp index.html index.htm;

        }

    }

 6.2.4 测试
分别修改两个tomcat下的webapps/ROOT/index.jsp的内容，使用tomcat1和tomcat2两个服务首页显示不同的内容，如下：

tomcat1下的index.jsp修改后：

![](https://s1.ax1x.com/2020/06/13/tv4iCT.png)

tomcat2下的index.jsp修改后：
![](https://s1.ax1x.com/2020/06/13/tv4F8U.png)



 

分别访问aaa.test.com、bbb.test.com测试反向代理。

请求访问aaa.test.com通过nginx代理访问tomcat1，请求访问bbb.test.com通过nginx代理访问tomcat2。


### 5 负载均衡
##### 5.1 什么是负载均衡
负载均衡 建立在现有网络结构之上，它提供了一种廉价有效透明的方法扩展网络设备和服务器的带宽、增加吞吐量、加强网络数据处理能力、提高网络的灵活性和可用性。

负载均衡，英文名称为Load Balance，其意思就是分摊到多个操作单元上进行执行，例如Web服务器、FTP服务器、企业关键应用服务器和其它关键任务服务器等，从而共同完成工作任务。

 

##### 5.2 nginx实现负载均衡

nginx作为负载均衡服务器，用户请求先到达nginx，再由nginx根据负载配置将请求转发至 tomcat服务器。

nginx负载均衡服务器：192.168.101.3

tomcat1服务器：192.168.101.5

tomcat2服务器：192.168.101.6
![](https://s1.ax1x.com/2020/06/13/tv4C5V.png)

##### 5.3 配置
根据上边的需求在nginx.conf文件中配置负载均衡，如下：

 

upstream tomcat_server_pool{

        server 192.168.101.5:8080 weight=10;

        server 192.168.101.6:8080 weight=10;

        }

 

    server {

        listen 80;

        server_name aaa.test.com;

        location / {

                 proxy_pass http://tomcat_server_pool;

                 index index.jsp index.html index.htm;

        }

    }

 
##### 5.4 测试

请求aaa.test.com，通过nginx负载均衡，将请求转发到tomcat服务器。

通过观察tomcat的访问日志或tomcat访问页面即可知道当前请求由哪个tomcat服务器受理。
