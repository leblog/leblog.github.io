---
title: 在Ubuntu16.04中安装hexo
top: false
cover: false
toc: true
mathjax: true
date: 2020-05-12 17:22:59
password:
summary:
tags: Ubuntu
categories:
---
在Ubuntu16.04中安装hexo出现一系列的问题，总结一下安装hexo的步骤;

首先安装noejs，Ubuntu源中的nodejs时旧版本，所以需要在安装后更新nodejs;
```
 > sudo apt-get install nodejs
 sudo apt install nodejs-legacy
 sudo apt install npm
 ```


 
更换成淘宝的镜像，否则非常慢

  ``sudo npm config set registry https://registry.npm.taobao.org``


可以通过 sudo npm config list 查看是否生效

安装更新版本的工具N

  ``sudo npm install n -g``


更新版本

  ``sudo n stable``


可以看到有 installed：版号，说明更新成功

安装hexo
        
  ``sudo npm install -g hexo``

    


