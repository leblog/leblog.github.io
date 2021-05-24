---
title: Java分布式的创建
top: false
cover: false
toc: true
mathjax: true
date: 2019-04-08 21:50:53
password:
summary:
tags: [Java,分布式]
categories: 分布式
---


## 注册中心的创建

1、建立注册中心(EurekaServer)，需要引入依赖。
Spring Cloud Discovery --> Eureka Server

2、在项目src-->main-->java-->com.XXX.XXXXX-->找到EurekaServerApplication(项目名字+Application)
中的类方法上加@EnableEurekaServer注解。

3、找到项目中的application.properties，在其中加入以下语句：

```
#端口号设置
server.port=8080
#注册中心服务记录地址
eureka.client.service-url.defaultZone=http://localhost:8080/eureka
#记录注册信息(记名字)
eureka.client.fetch-registry=false
#服务注册到注册中心
eureka.client.register-with-eureka=false#端口号设置
server.port=8080
#注册中心服务记录地址
eureka.client.service-url.defaultZone=http://localhost:8080/eureka
#记录注册信息(记名字)
eureka.client.fetch-registry=false
#服务注册到注册中心
eureka.client.register-with-eureka=false
```

## 注册中心创建完毕

**生产者的建立**

1、建立生产者(producer),需要引入依赖。
Web--> Spring Web
SQL--> JDBC API , MyBatis Framework , MySQL Driver
Spring Cloud Discovery--> Eureka Discovery Client

2、在项目src-->main-->java-->com.XXX.XXXXX-->找到MyproviderApplication(项目名字+Application)
在类方法上加@EnableEurekaClient注解

3、找到项目中的application.properties，在其中加入以下语句：
```
#设置端口号
server.port=8081
# 数据库连接属性
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.url=jdbc:mysql://localhost:3306/test(数据库名字)?serverTimezone=UTC(时区)
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
# 给实体类起别名
mybatis.type-aliases-package=com.example.demo.bean
# 扫描mapper文件
mybatis.mapper-locations=classpath:mapper/*.xml
#给项目起名字
spring.application.name=myprovider
#注册项目
eureka.client.service-url.defaultZone=http://localhost:8080/eureka
```

PS：如需一个对象为参数则需要@RequestBody注解，如果是其他数据类型则需要添加@RequestParam("XXX")注解，

PS:XXX就是参数的名字

## 消费者的建立
1、建立消费者(consumer),需要引入依赖。
Web--> Spring Web
Template Engines--> Thymeleaf
Spring Cloud Discovery--> Eureka Discovery Client
Spring Cloud Routing-->OpenFeign

2、在项目src-->main-->java-->com.XXX.XXXXX-->找到MyconsumerApplication(项目名字+Application)
在类方法上加@EnableEurekaClient,@EnableFeignClients这两个注解

3、找到项目中的application.properties，在其中加入以下语句：

```
#设置端口号
server.port=8082
#给项目起名字
spring.application.name=myconsumer
#注册项目
eureka.client.service-url.defaultZone=http://localhost:8080/eureka
```

4、在消费者中建立一个文件夹(名字是Feign)在文件夹中建立类(名字为XXXFeign)，
在其中编写远程调用相关配置

```
@FeignClient("myprovider")
public interface TestFeign {
    @RequestMapping("index")
    public String a(@RequestParam("uname") String uname);
}
```

5、在Controllet中调用Feign
```
@Controller
public class UserController {
    @Autowired
    Ufeign ufeign;
    @RequestMapping("ajaxsel")
    @ResponseBody
    public List<User> l(){
        List<User> list=ufeign.a();
        return list;
    }
```

最后注意:
其中因为会遇到实体类的问题，所以需要创建公共实体类。
步骤为：
1、创建一个Maven项目，在Create from archetpe复选框前勾选上。

2、在下面的列表中找到org.apache.maven.archetypes:maven-archetype-quickstart,选中。然后点击next

3、接下来分别输入类型(groupId)，名字(artifactId),版本号根据自己的需求决定是否改变。点击下一步即可创建公共实体类

4、之后会让你确认信息，点击下一步即可创建公共实体类。

5、在pom.xml中只保留以下信息

```
<?xml version="1.0" encoding="UTF-8"?>
 
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
 
  <groupId>bean</groupId>
  <artifactId>module</artifactId>
  <version>1.0-SNAPSHOT</version>
 
</project>
```

6、在src-->main-->java-->bean创建公用的实体类。

7、删除其中的test文件夹

8、在右边找到Maven，点击展开后，找到项目名下面的Lifecycle展开后，
找到下面的install，双击。当出现以下内容时即创建成功。

```
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  1.369 s
[INFO] Finished at: 2019-10-26T16:57:15+08:00
[INFO] ------------------------------------------------------------------------

Process finished with exit code 0
```