---
title: HTTP 请求的 GET 与 POST 方式的区别
top: false
cover: false
toc: true
mathjax: true
date: 2018-07-16 19:04:56
password:
summary:
tags: [学习笔记,小知识]
categories: 学习笔记
---


# HTTP 请求的 GET 与 POST 方式的区别

> GET和POST是什么？HTTP协议中的两种发送请求的方法。

> HTTP是什么？HTTP是基于TCP/IP的关于数据如何在万维网中如何通信的协议。

- HTTP的底层是TCP/IP。所以GET和POST的底层也是TCP/IP，也就是说，GET/POST都是TCP链接。


- GET和POST本质上就是TCP链接，并无差别。

### GET和POST还有一个重大区别：

- GET产生一个TCP数据包；POST产生两个TCP数据包。

### 小栗子:

- 对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；

- 对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）。

因为POST需要两步，时间上消耗的要多一点，看起来GET比POST更有效。因此Yahoo团队有推荐用GET替换POST来优化网站性能。但这是一个坑！跳入需谨慎。为什么？

1.  GET与POST都有自己的语义，不能随便混用。
2. 据研究，在网络环境好的情况下，发一次包的时间和发两次包的时间差别基本可以无视。而在网络环境差的情况下，两次包的TCP在验证数据包完整性上，有非常大的优点。

3.  并不是所有浏览器都会在POST中发送两次包，Firefox就只发送一次。



**官方说法：**

> - 根据 HTTP 规范，GET 用于信息获取，而且应该是安全的和幂等的。
> - 根据 HTTP 规范，POST 表示可能修改变服务器上的资源的请求。
> - 首先是 "GET 方式提交的数据最多只能是 1024 字节"，因为 GET 是通过 URL 提交数据，那么 GET 可提交的数据量就跟 URL 的长度有直接关系了。而实际上，URL 不存在参数上限的问题，HTTP 协议规范没有对 URL 长度进行限制。这个限制是特定的浏览器及服务器对它的限制。IE 对 URL 长度的限制是 2083 字节(2K+35)。对于其他浏览器，如 Netscape、FireFox 等，理论上没有长度限制，其限制取决于操作系统的支持。注意这是限制是整个 URL 长度，而不仅仅是你的参数值数据长度。
> - POST 是没有大小限制的，HTTP 协议规范也没有进行大小限制

