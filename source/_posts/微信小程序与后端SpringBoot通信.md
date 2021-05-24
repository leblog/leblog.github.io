---
title: 微信小程序与后端SpringBoot通信
top: false
cover: false
toc: true
mathjax: true
date: 2019-02-03 00:31:21
password:
summary:
tags: [SpringBoot,微信小程序]
categories: SpringBoot
---


# 微信小程序与后端SpringBoot通信

### 案例概述
微信小程序请求后端SpirngBoot,中间使用Ngrok做内网穿透.
![](https://note.youdao.com/yws/public/resource/a7b28e89afc8e429d20c7293f6faa483/xmlnote/CE885778600E42938491F27E91BC8E79/2661)

### 内网穿透Ngrok配置
### 下载Ngrok
> https://ngrok.com/download

### 注册并配置Ngrok认证
注册完Ngrok之后进入个人主页在Auth页面找到自己的验证码,然后打开Ngrok认证即可

![](https://s2.ax1x.com/2019/07/03/ZtnNxe.png)

### 配置端口和协议

我这里的端口是8181,因为我Tomcat的端口是8181\

> ngrok http 8181

### Ngrok配置完成
配置完成之后Ngrok会为我们提供两个链接,一个是http协议的一个市https协议的.

Ngrok的作用说白了就是将你本地某个端口上运行的服务暴露在了公网上.

这里的穿透指的就是将内网中的服务穿过防火墙.
![](https://note.youdao.com/yws/public/resource/a7b28e89afc8e429d20c7293f6faa483/xmlnote/ED9712F8F49443C1B0A9D65EAA8B6E8A/2665)


### 后端SpringBoot
### Controller
接收微信小程序发来的请求,并根据请求做出响应
```
package le.controll;

import le.domain.Info;
import le.utils.JSONResult;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

/**
* @program: SpringBootIntrodoction
* @description:
* @author: Mr.Han
* @create: 2019-01-26 22:16
**/
@Controller
public class QuickController2 {

    @RequestMapping("/info")
    @ResponseBody
    public JSONResult quick(Info info) {
        System.out.println(info.toString());
        return JSONResult.ok(info);
    }
}
```
### 实体类
```
package le.domain;


import java.io.Serializable;

/**
* @program: SpringBootIntrodoction
* @description: 测试实体类
* @author: Mr.Han
* @create: 2019-02-01 14:13
**/
public class Info implements Serializable {
    private String name;
    private String personName;
    private Integer age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPersonName() {
        return personName;
    }

    public void setPersonName(String personName) {
        this.personName = personName;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Info{" +
                "name='" + name + '\'' +
                ", personName='" + personName + '\'' +
                ", age=" + age +
                '}';
    }
}
```

### JSON工具类
```
package chen.utils;

import chen.domain.Info;
import com.fasterxml.jackson.databind.util.JSONPObject;
import org.springframework.boot.configurationprocessor.json.JSONObject;

/**
* @program: SpringBootIntrodoction
* @description: 实体类转换成JSON
* @author: Mr.Han
* @create: 2019-02-01 14:17
**/
public class JSONResult {

    // 响应业务状态
    private Integer status;

    // 响应消息
    private String msg;

    // 响应中的数据
    private Object data;

    private String ok;    // 不使用

    public static JSONResult build(Integer status, String msg, Object data) {
        return new JSONResult(status, msg, data);
    }

    public static JSONResult ok(Object data) {
        return new JSONResult(data);
    }

    public static JSONResult ok() {
        return new JSONResult(null);
    }

    public static JSONResult errorMsg(String msg) {
        return new JSONResult(500, msg, null);
    }

    public static JSONResult errorMap(Object data) {
        return new JSONResult(501, "error", data);
    }

    public static JSONResult errorTokenMsg(String msg) {
        return new JSONResult(502, msg, null);
    }

    public static JSONResult errorException(String msg) {
        return new JSONResult(555, msg, null);
    }

    public JSONResult() {

    }

    public JSONResult(Integer status, String msg, Object data) {
        this.status = status;
        this.msg = msg;
        this.data = data;
    }

    public JSONResult(Object data) {
        this.status = 200;
        this.msg = "OK";
        this.data = data;
    }

    public Boolean isOK() {
        return this.status == 200;
    }

    public Integer getStatus() {
        return status;
    }

    public void setStatus(Integer status) {
        this.status = status;
    }

    public String getMsg() {
        return msg;
    }

    public void setMsg(String msg) {
        this.msg = msg;
    }

    public Object getData() {
        return data;
    }

    public void setData(Object data) {
        this.data = data;
    }

    public String getOk() {
        return ok;
    }

    public void setOk(String ok) {
        this.ok = ok;
    }

}
```
### 微信小程序端
### 视图
```
<view bindtap="clickMe">点击发送请求</view>
```
绑定了一个bindtap事件,点击的时候发送请求

### JS代码
```
// pages/requestinterface/requestinterface.js
Page({

  /**
  * 页面的初始数据
  */
  data: {

  },
  clickMe: function() {
    wx.request({
      url: 'ngrok公网接口',
      data: {
        personName: "张三的父亲",
        name: "张三",
        age: 18
      },
      header: {
        'content-type': 'application/json' 
      },
      success(res) {
        console.log(res.data)
      }
    })
  }

})
```
### 完整的流程

![](https://note.youdao.com/yws/public/resource/a7b28e89afc8e429d20c7293f6faa483/xmlnote/7DA9DB9E98644776B0AD870AAAC8523C/2667)

### 特别提醒
因为我们使用的是Ngrok做的内网穿透,微信小程序默认识别出Ngrok的接口时非法的.
![](https://note.youdao.com/yws/public/resource/a7b28e89afc8e429d20c7293f6faa483/xmlnote/1A5B10B7B372467BA836F71645423091/2669)


这时候我们就必须要**设置不校验合法域名**

![](https://note.youdao.com/yws/public/resource/a7b28e89afc8e429d20c7293f6faa483/xmlnote/5C3B2976BF574C7780F48218C16B37B3/2671)


