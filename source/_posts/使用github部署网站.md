---
title: 使用github部署网站
top: false
cover: false
toc: true
mathjax: true
date: 2018-04-23 23:30:52
password:
summary: 这篇博客对GitHub界面的信息介绍的非常详细
		特别适合小白上手！！！码字不易希望多多支持
tags: [Github,学习笔记]
categories: Github
---

# 使用GitHub部署网站 #

**在部署网站之前，先要有一个GitHub账号，熟悉一些git命令，注册GitHub账号和使用git命令可以参考下面的博客，在博客中介绍的非常详细，我也不做过多的介绍**
<hr/>
从0开始学习GitHub系列汇总：[http://pan.baidu.com/s/1hsn57YO](http://pan.baidu.com/s/1hsn57YO)

注册好GitHub账号并且完善用户信息后可以得到一个下图所示的界面，下图是我的GitHub界面，其中界面中的信息介绍可以参考，`从0开始学习 GITHUB 系列之「加入 GITHUB」`这篇博客对GitHub界面的信息介绍的非常详细

![](https://i.imgur.com/rnbszof.png)

在GitHub上部署网站：

**第一步**：单击Repositories，其中Repositories在GitHub上表示的是仓库，在GitHub上每个项目都存放在仓库里，一个仓库保存一个项目
![](https://i.imgur.com/pPjslYS.jpg)

**第二步**：单击根据图中的提示填写信息，信息填写完成后单击Create respository按钮创建仓库
![](https://i.imgur.com/zjbd2WZ.jpg)

**第三步**：单击创建好仓库后会自动跳转到下图所示的界面，在界面中单击Settings
![](https://i.imgur.com/KdK0YwY.jpg)

**第四步**：提示在下面的操作中需要电脑中安装了git，并且熟悉几个简单的git命令，关于git的安装以及git命令的使用可以参考`从0开始学习 GITHUB 系列之「GIT 速成」`，这篇博客将git介绍的非常通俗易懂，安装好git后，先在电脑中创建一个文件夹用于保存从Github中克隆下来的仓库，我建的文件夹叫做demo，在d:\Git路径下，打开命令行进入demo文件夹下
![](https://i.imgur.com/T8eLnrI.png)
**第五步**在 命令行中执行`https://github.com/leblog/test.git`命令

其中`git clone `表示要克隆一个项目，后面的`https://github.com/leblog/test.git`表示项目地址，该地址是由第十二步操作获得的，当在最后一行出现了100%表示，远程仓库已经成功的克隆到了本地
![](https://i.imgur.com/OIRdznD.png)
**第六步**：打开demo文件夹，可以看到在文件夹中多了一个test文件，该文件正是刚刚在GitHub中创建的仓库

![](https://i.imgur.com/UnaGLvt.png)
**第七步**：打开文件，并且将需要上传到GitHub上的网站添加到该文件中
![](https://i.imgur.com/6nWYnck.png)
**第八步**：打开命令行，并且进入test文件夹下，并且执行 `git add .`命令，此命令表示将需要提交到git中的文件先添加到缓存
![](https://i.imgur.com/N5bRudR.png)
**第九步**：执行 `git commit -m "first commit ."`，此命令表示将文件提交到git中，下面显示的都是提交到git中的文件

![](https://i.imgur.com/dopR8lM.png)
**第十步**：执行` git push origin master`命令，将文件`push`到GitHub上的master分支上，当出现下图所示的提示信息时，表示网站已经成功的提交到了GitHub上
![](https://i.imgur.com/yM8aV3c.png)
**第十一步**：回到Github上的test仓库，可以看到文件已经全部提交上来了
<hr/>
通过观察网址可知，网址的格式为 https:// + GitHub的用户名 + .github.io/ + 仓库的名称

![](https://i.imgur.com/xhbPnpJ.png)


