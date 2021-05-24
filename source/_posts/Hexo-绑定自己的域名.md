---
title: Hexo 绑定自己的域名
top: false
cover: false
toc: true
mathjax: true
date: 2018-01-17 20:11:04
password:
summary:
tags: [博客，教程]
categories: 博客
---


# Hexo 绑定自己的域名

>前提，你得有一个域名，有些域名需要备案后才能用。
### 在域名解析添加记录

如果你用你顶点域名（如：hanlele.cn)，就添加一条主机记录为@的，如果你用www子域名（如：www.hnalele.cn）,github绑定自己的域名只支持这两种，不支持其他子域名，你可以去github的help查看

![域名解析](https://note.youdao.com/yws/public/resource/a7b28e89afc8e429d20c7293f6faa483/xmlnote/8C10B38C3C154904BF65E557EFE0FD53/2749)



- 记录类型一定要为 CNAME - 这种类型，只有这样你的域名才能指向你的github
记录值填 yourname.github.io

### 在github添加自定义域名
![](https://note.youdao.com/yws/public/resource/a7b28e89afc8e429d20c7293f6faa483/xmlnote/291DCB7301054795AE30744F12253BB7/2754)

### 配置hexo的_config.yml

找到url设置，添加你的域名
```
# URL 链接设置
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://www.hanlele.cn
root: /
permalink: :year/:month/:day/:title/
permalink_defaults: 
```

### 上传CNAME文件

光执行上面三个步骤还是不够，每次你上传更新时，你在github设置的域名可能会丢失，所以要上传一个CNAME文件，让github记住你添加的域名：
先创建一个名为CNAME的文件，没有后缀，再在文件中写上你的域名（如：www.hanlele.cn）,然后把这个文件放在/hexo/source目录下，上传就行了。

# hexo 搭建个人博客部署环节spawn failed及解决


 我的做法是：
 - 1、先把git加入系统环境变量；
- 2、再将博客目录里的.git文件夹删除(注意不要永久删除不然有可能数据会丢失)
- 3.、命令步骤：
> hexo clean
>hexo g
> hexo  d


4、至此，解决

最后放上我的报错截图：

建议：不要使用cmd上传，用Git bash或其他
![](https://note.youdao.com/yws/public/resource/a7b28e89afc8e429d20c7293f6faa483/xmlnote/2A44E55BB64444CB8774E1EFBB468FFD/2784)
