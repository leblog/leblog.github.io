---
title: 阿里巴巴Java方向面试题汇总（含答案）
top: false
cover: false
toc: true
mathjax: true
date: 2018-05-01 21:21:54
password:
summary:
tags: [JAVA,面试]
categories: JAVA
---


# 阿里巴巴Java方向面试题汇总（含答案） #

涉及了从Java内置的基础数据结构、常用的服务器知识、Java网络编程相关的知识，再到Java的内存模型、Java常用编程框架等各个方面的内容，希望能够帮助大家回顾Java的基础内容，进而查漏补缺，完善自身的知识体系。

## 一、String, StringBuffer, StringBuilder的区别是什么？String为什么是不可变的？ ##
1. String是字符串常量，StringBuffer和StringBuilder都是字符串变量。后两者的字符内容可变，而前者创建后内容不可变。
1. String不可变是因为在JDK中String类被声明为一个final类。
1. StringBuffer是线程安全的，而StringBuilder是非线程安全的。

**补充说明**：线程安全会带来额外的系统开销，所以StringBuilder的效率比StringBuffer高。如果对系统中的线程是否安全很掌握，可用StringBuffer，在线程不安全处加上关键字Synchronize。

## 二、Vector, ArrayList, LinkedList的区别是什么？ ##
1. Vector、ArrayList都是以类似数组的形式存储在内存中，LinkedList则以链表的形式进行存储。
1. List中的元素有序、允许有重复的元素，Set中的元素无序、不允许有重复元素。
1. Vector线程同步，ArrayList、LinkedList线程不同步。
1. LinkedList适合指定位置插入、删除操作，不适合查找；ArrayList、Vector适合查找，不适合指定位置的插入、删除操作。
1. ArrayList在元素填满容器时会自动扩充容器大小的约50%，而Vector则是100%，因此ArrayList更节省空间。

## 三、HashTable, HashMap， TreeMap的区别是什么？ ##
1. HashTable线程同步，HashMap非线程同步。
1. HashTable不允许<键,值>有空值，HashMap允许<键,值>有空值。
1. HashTable使用Enumeration，HashMap使用Iterator。
1. HashTable中hash数组的默认大小是11，增加方式的old*2+1，HashMap中hash数组的默认大小是16，增长方式一定是2的指数倍。
1. TreeMap能够把它保存的记录根据键排序，默认是按升序排序。

**补充说明**：以上三个问题所涉及的都是Java语言中的一些比较高级的数据结构，从字符串相关到容器再到哈希表和树等数据结构，因此我们在学习Java语言的时候，也需要更加深入地去对比比较类似的数据结构的使用场景以及其优缺点。

## 四、Tomcat，Apache，JBoss的区别？ ##
1. Apache是HTTP服务器，Tomcat是Web服务器，JBoss是应用服务器。
1. Apache解析静态的Html文件；Tomcat可解析jsp动态页面、也可充当
1. 容器。

**补充说明**：对于服务器而言，在面试中可能并不会过多涉及，相对而言，面小易认为像是Liunx、Tomcat这些背后的原理可能更受面试官的青睐。

## 五、GET，POST请求之间的区别？ ##

	基础知识：HTTP的请求格式如下。
	主要包含三个信息：1、请求的类型（GET或POST），2、要访问的资源（如resimga.jif），3、HTTP版本（http/1.1）

**区别：**

1. Get是从服务器端获取数据，Post则是向服务器端发送数据。
1. 在客户端，Get方式通过URL提交数据，在URL地址栏可以看到请求消息，该消息被编码过；Post数据则是放在Html header内提交。
1. 对于Get方式，服务器端用Request.QueryString获取变量的值；对用Post方式，服务器端用Request.Form获取提交的数据值。
1. Get方式提交的数据最多1024字节，而Post则没有限制。
1. Get方式提交的参数及参数值会在地址栏显示，不安全，而Post不会，比较安全。

## 六、Session, Cookie的区别是什么？ ##

1. Session由应用服务器维护的一个服务器端的存储空间；Cookie是客户端的存储空间，由浏览器维护。
1. 用户可以通过浏览器设置决定是否保存Cookie，而不能决定是否保存Session，因为Session是由服务器端维护的。
1. Session中保存的是对象，Cookie中保存的是字符串。
1. Session和Cookie不能跨窗口使用，每打开一个浏览器系统会赋予一个SessionID，此时的SessionID不同，若要完成跨浏览器访问数据，可以使用 Application。
1. Session、Cookie都有失效时间，过期后会自动删除，减少系统开销。

## 七、HTTP 报文包含内容 ##

主要包含四部分：

1. request line
1. header line
1. blank line
1. request body

**补充说明**：上面的三个问题是网络编程的基础知识问题，作为Java工程师也需要掌握HTTP的知识，而如今HTTPS同样也成为了标准，也需要大家进一步了解。此外，相对于大家在课本或者课堂中所学习的HTTP 1.0/1.1这些协议而言，很多公司已经迈入了HTTP 2.0时代，因此两者之间的差别也需要我们进一步了解。

## 八、Servlet的生命周期 ##

大致分为4部：Servlet类加载–>实例化–>服务–>销毁

Tomcat中Servlet的时序图如下所示：

![](https://i.imgur.com/6t8q318.jpg)

1. Web Client向Servlet容器(Tomcat)发出HTTP请求。
1. Servlet容器接收Client端的请求。
1. Servlet容器创建一个HttpRequest对象，将Client的请求信息封装到这个对象中。
1. Servlet创建一个HttpResponse对象。
1. Servlet调用HttpServlet对象的service方法，把HttpRequest对象和HttpResponse对象作为参数传递给HttpServlet对象中。
1. HttpServlet调用HttpRequest对象的方法，获取Http请求，并进行相应处理。
1. 处理完成HttpServlet调用HttpResponse对象的方法，返回响应数据。
1. Servlet容器把HttpServlet的响应结果传回客户端。

其中的3个方法说明了Servlet的生命周期：

1. init()：负责初始化Servlet对象。
1. service()：负责响应客户端请求。
1. destroy()：当Servlet对象推出时，负责释放占用资源。

## 九、Statement与PreparedStatement的区别,什么是SQL注入，如何防止SQL注入？ ##
1. PreparedStatement支持动态设置参数，Statement不支持。
1. PreparedStatement可避免如类似 单引号 的编码麻烦，Statement不可以。
1. PreparedStatement支持预编译，Statement不支持。
1. 在SQL语句出错时PreparedStatement不易检查，而Statement则更便于查错。
1. PreparedStatement可防止SQL助于，更加安全，而Statement不行。

**补充说明-什么是SQL注入以及应对策略：** 通过SQL语句的拼接达到无参数查询数据库数据目的的方法。如将要执行的SQL语句为 select * from table where name = “+appName+”，利用appName参数值的输入，来生成恶意的SQL语句，如将[‘or’1’=‘1’] 传入可在数据库中执行。因此可以采用PrepareStatement来避免SQL注入，在服务器端接收参数数据后，进行验证，此时PrepareStatement会自动检测，而Statement不行，需要手工检测。

## 十、sendRedirect, foward区别 ##
1. foward是服务器端控制页面转向，在客户端的浏览器地址中不会显示转向后的地址；sendRedirect则是完全的跳转，浏览器中会显示跳转的地址并重新发送请求链接。原理：forward是服务器请求资源，服务器直接访问目标地址的URL，把那个URL的响应内容读取过来，然后再将这些内容返回给浏览器，浏览器根本不知道服务器发送的这些内容是从哪来的，所以地址栏还是原来的地址。
1. redirect是服务器端根据逻辑，发送一个状态码，告诉浏览器重新去请求的那个地址，浏览器会用刚才的所有参数重新发送新的请求。

**补充说明**：以上的三个问题在之前网络相关的知识上更进一步，上升到了Java网络编程的相关知识，这部分意在考察面试者对于Java网络编程相关知识的掌握程度。

## 十一、谈谈Hibernate的理解，一级和二级缓存的作用，在项目中Hibernate都是怎么使用缓存的？ ##
Hibernate是一个开发的对象关系映射框架（ORM）。它对JDBC进行了非常对象封装，Hibernate允许程序员采用面向对象的方式来操作关系数据库。

**Hibernate的优点：**

1. 程序更加面向对象
1. 提高了生产率
1. 方便移植
1. 无入侵性

**Hibernate的缺点：**

1. 效率比JDBC略差
1. 不适合批量操作
1. 只能配置一种关联关系

**Hibernate有四种查询方式：**

1. get、load方法，根据ID号查询对象。
1. Hibernate Query Language, HQL
1. 标准查询语言
1. 通过SQL查询

**Hibernate工作原理：**

1. 配置Hibernate对象关系映射文件、启动服务器
1. 服务器通过实例化Configuration对象，读取hibernate.cfg.xml文件的配置内容，并根据相关的需求建好表以及表之间的映射关系。
1. 通过实例化的Configuration对象建立SessionFactory实例，通过SessionFactory实例创建Session对象。
1. 通过Session对象完成数据库的增删改查操作。

**Hibernate中的状态转移：**

*临时状态（Transient）*

1. 不处于SESSION缓存中
1. 数据库中没有对象记录

**补充说明-Java是如何进入临时状态的：**1、通过new语句创建一个对象时。2、刚调用Session的delete()方法时，从Session缓存中删除一个对象时。

*持久化状态(Persisted)*
1、处于Session缓存中
2、持久化对象数据库中没有对象记录
3、Session在特定的时刻会保存两者同步

补**充说明-Java如何进入持久化状态**：1、Session的save()方法。2、Session的load().get()方法返回的对象。3、Session的find()方法返回的list集合中存放的对象。4、Session的update().save()方法。

*流离状态（Detached）*
1、不再位于Session缓存中
2、游离对象由持久化状态转变而来，数据库中还没有相应记录。

**补充说明-Java如何进入流离状态：**

1、Session的close()。2、 Session的evict()方法，从缓存中删除一个对象。

具体如下图所示：
![](https://i.imgur.com/StmlgBX.png)

Hibernate中的缓存主要有Session缓存（一级缓存）和SessionFactory缓存（二级缓存，一般由第三方提供）。

## 十二、谈谈Hibernate与iBatis的区别，哪个性能会更高一些 ##

1. Hibernate偏向于对象的操作达到数据库相关操作的目的；而iBatis更偏向于SQL语句的优化。
1. Hibernate的使用的查询语句是自己的HQL，而iBatis则是标准的SQL语句。
1. Hibernate相对复杂，不易学习；iBatis类似SQL语句，简单易学。

**性能方面：**
1. 如果系统数据处理量巨大，性能要求极为苛刻时，往往需要人工编写高性能的SQL语句或存错过程，此时iBatis具有更好的可控性，因此性能优于Hibernate。
1. 同样的需求下，由于Hibernate可以自动生成HQL语句，而iBatis需要手动写SQL语句，此时采用Hibernate的效率高于iBatis。

## 十三、对Spring的理解，项目中都用什么？怎么用的？对IOC、和AOP的理解及实现原理。 ##
Spring是一个开源框架，处于MVC模式中的控制层，它能应对需求快速的变化，其主要原因它有一种面向切面编程（AOP）的优势，其次它提升了系统性能，因为通过依赖倒置机制（IOC），系统中用到的对象不是在系统加载时就全部实例化，而是在调用到这个类时才会实例化该类的对象，从而提升了系统性能。这两个优秀的性能使得Spring受到许多J2EE公司的青睐，如阿里中使用最多的也是Spring相关技术。

**Spring的优点：**

1. 降低了组件之间的耦合性，实现了软件各层之间的解耦。
1. 可以使用容易提供的众多服务，如事务管理，消息服务，日志记录等。
1. 容器提供了AOP技术，利用它很容易实现如权限拦截、运行期监控等功能。

Spring中AOP技术是设计模式中的动态代理模式。只需实现jdk提供的动态代理接口InvocationHandler，所有被代理对象的方法都由InvocationHandler接管实际的处理任务。面向切面编程中还要理解切入点、切面、通知、织入等概念。

Spring中IOC则利用了Java强大的反射机制来实现。所谓依赖注入即组件之间的依赖关系由容器在运行期决定。其中依赖注入的方法有两种，通过构造函数注入，通过set方法进行注入。

## 十四、描述Struts的工作流程 ##

1. 在web应用启动时，加载并初始化ActionServlet，ActionServlet从struts-config.xml文件中读取配置信息，将它们存放到各个配置对象中。
1. 当ActionServlet接收到一个客户请求时，首先检索和用户请求相匹配的ActionMapping实例，如果不存在，就返回用户请求路径无效信息。
1. 如果ActionForm实例不存在，就创建一个ActionForm对象，把客户提交的表单数据保存到ActionForm对象中。
1. 根据配置信息决定是否需要验证表单，如果需要，就调用ActionForm的validate()方法，如果ActionForm的validate()方法返回null或返回一个不包含ActionMessage的ActionErrors对象，就表示表单验证成功。
1. ActionServlet根据ActionMapping实例包含的映射信息决定请求转发给哪个Action，如果相应的Action实例不存在，就先创建一个实例，然后调用Action的execute()方法。

**补充说明**：以上部分的相关问题考察面试者在实际软件开发中所使用的Java语言相关框架以及对于框架原理的了解程度，这一部分我们需要注意一些常见的框架，不仅需要知道它们是干什么的，还需要知道它们背后的原理，常会问到的框架有Spring Boot/Spring Cloud全家桶、Hibernate、MyBaits、Netty、Kafka等，最重要的还有阿里巴巴开源的Apache Dubbo框架。

## 十五、关于Java内存模型，一个对象（两个属性，四个方法）实例化100次，现在内存中的存储状态，几个对象，几个属性，几个方法。由于Java中new出来的对象都是放在堆中，所以如果要实例化100次，将在堆中产生100个对象，一般对象与其中的属性、方法都属于一个整体，但如果 属性和方法是静态的，就是用static关键字声明的，那么属于类的属性和方法永远只在内存中存在一份 ##。


## 十六、反射讲一讲，主要是概念,都在哪需要反射机制，反射的性能，如何优化？ ##

**反射机制的定义：**

是在运行状态中，对于任意的一个类，都能够知道这个类的所有属性和方法，对任意一个对象都能够通过反射机制调用一个类的任意方法，这种动态获取类信息及动态调用类对象方法的功能称为java的反射机制。

**反射的作用：**

1. 动态地创建类的实例，将类绑定到现有的对象中，或从现有的对象中获取类型。
1. 应用程序需要在运行时从某个特定的程序集中载入一个特定的类。

## 十七、线程同步，并发操作怎么控制？ ##

Java中可在方法名前加关键字syschronized来处理当有多个线程同时访问共享资源时候的问题。syschronized相当于一把锁，当有申请者申请该资源时，如果该资源没有被占用，那么将资源交付给这个申请者使用，在此期间，其他申请者只能申请而不能使用该资源，当该资源被使用完成后将释放该资源上的锁，其他申请者可申请使用。并发控制主要是为了多线程操作时带来的资源读写问题。如果不加以空间可能会出现死锁，读脏数据、不可重复读、丢失更新等异常。

**并发操作可以通过加锁的方式进行控制，锁又可分为乐观锁和悲观锁。**

**悲观锁：**

悲观锁并发模式假定系统中存在足够多的数据修改操作，以致于任何确定的读操作都可能会受到由个别的用户所制造的数据修改的影响。也就是说悲观锁假定冲突总会发生，通过独占正在被读取的数据来避免冲突。但是独占数据会导致其他进程无法修改该数据，进而产生阻塞，读数据和写数据会相互阻塞。

**乐观锁：**

乐观锁假定系统的数据修改只会产生非常少的冲突，也就是说任何进程都不大可能修改别的进程正在访问的数据。乐观并发模式下，读数据和写数据之间不会发生冲突，只有写数据与写数据之间会发生冲突。即读数据不会产生阻塞，只有写数据才会产生阻塞。

**补充说明**：最后的几个问题又回到了Java内存模型以及进程、线程的底层知识上，其实无论是对于Java网络编程也好，还是对于Java框架的使用也好，这都离不开Java语言底层的技术支撑，因此了解底层知识是做好优化的重中之重。