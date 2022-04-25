---
title: 禁用Chrome缓存功能
top: false
cover: false
toc: true
mathjax: true
date: 2021-05-25 17:35:23
password:
summary:
tags: [web]
categories: web
---


### 如何禁用Chrome 缓存功能

一般，禁止Chrome浏览器的缓存功能有几种方式。



1. 使用隐身模式Shift + Control + N. 这种方法只能在打开的页面上消除之前缓存的影响，对于打开隐身模式之后做的任何更改都无法刷新缓存，因此也不甚实用。
   ![1650879612192](https://upyun.hanlele.cn/img/win11/1650879612192.png)
2. 在DevTool (Shift + Control + I) 中Disable Cache. 这种方法基本能够做到完全禁止缓存，然而缺点是必须要将开发模式一直打开，占用屏幕空间。而且，每打开一个标签页都需要再进行一番操作，相当不便利。
   ![image-20220425181752578](https://upyun.hanlele.cn/img/win11/image-20220425181752578.png)

3. 更改Chrome 属性,右键浏览器,悬着属性在目标栏中加上 `–-disk-cache-size=1`  **切记前面有空格**

4. 使用插件的方式

   > 今天我们发现了这样一款插件，可以 完美实现这一功能。插件名为Classic Cache Killer, 可以一键开启或者关闭缓存。插件的下载链接如下：https://chrome.google.com/webstore/detail/classic-cache-killer/kkmknnnjliniefekpicbaaobdnjjikfp

   安装插件完成浏览器又上方会有一个小图标,点击就会开关.非常方便....
   ![](https://upyun.hanlele.cn/img/win11/image-20220425182227252.png)