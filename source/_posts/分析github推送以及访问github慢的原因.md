---
title: 分析github推送以及访问github慢的原因
top: false
cover: false
toc: true
mathjax: true
date: 2021-07-29 22:49:54
password:
summary:
tags: [Git,Gihub]
categories: Gihub
---


# 分析github推送以及访问github慢的原因

## 分析推送慢

### 1. github.com服务器在境外,境内访问较慢

可以采用国内的镜像源做推送,

> **http镜像**
>
> https://github.com.cnpmjs.org
>
> 举例:https://github.com.cnpmjs.org/fhefh2015/Fast-GitHub.git
>
> **ssh镜像**
>
> git.zhlh6.cn
>
> 举例:git@git.zhlh6.cn:fhefh2015/Fast-GitHub.git

更换前

![image-20210730101231970](https://ali.frist-art.cn/wx/tianyan/photo/image-20210730101231970.png)

更换后

![image-20210730101314358](https://ali.frist-art.cn/wx/tianyan/photo/image-20210730101314358.png)

​	2.更换源步骤

```
1. git remote -vv //查看本地仓库源
❯ git remote -vv
origin  git@github.com:lexxxg/cxxx.git (fetch)
origin  git@github.com:lexxxg/cxxx.git (push)

2. git remote rm origin   //删除该分支

3. git remote add origin git@git.zhlh6.cn:lexxxg/cxxx.git//将其中github.com替换为git.zhlh6.cn

4. git remote -vv //再次查看本地仓库源
❯ git remote -vv
origin  git@github.com.cnpmjs.org:lexxxg/cxxx.git (fetch)
origin  git@github.com.cnpmjs.org:lexxxg/cxxx.git (push)
```

**恭喜你可以愉快地使用github clone 和 推送了**



## 分析访问慢

### 1.国内访问 GitHub 为什么很慢？

GitHub的CDN域名遭到DNS污染，导致无法连接使用 GitHub 的加速分发服务器，才使得国内访问速度很慢。

### 2.如何解决 DNS 污染？

通过修改 Hosts 文件，将域名解析直接指向 IP 地址来绕过 DNS 的解析，以此解决污染问题。

### 3.具体步骤

1、获取Github的ip地址

通过访问 https://www.ipaddress.com/ 这个网站来获取当前github最新的ip地址。

![image-20210730102334400](https://ali.frist-art.cn/wx/tianyan/photo/image-20210730102334400.png)

![image-20210730102427017](https://ali.frist-art.cn/wx/tianyan/photo/image-20210730102427017.png)

2. 修改 host 文件  位置:C:\Windows\System32\drivers\etc   

> 192.30.253.112      github.com
> 192.30.253.113      github.com
> 151.101.185.194     github.global.ssl.fastly.net

3. 更新dns缓存

> ipconfig /flushdns

