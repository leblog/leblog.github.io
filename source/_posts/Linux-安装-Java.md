---
title: Linux 安装 Java
top: false
cover: false
toc: true
mathjax: true
date: 2018-08-12 12:24:42
password:
summary:
tags: [Linux,教程]
categories: Linux
---
>此处以 JDK 1.8.0_152 为例

# 解压缩并移动到指定目录

### 解压缩
```
tar -zxvf jdk-8u152-linux-x64.tar.gz
```
### 创建目录

```
mkdir -p /usr/local/java
```
### 移动安装包

```
mv jdk1.8.0_152/ /usr/local/java/
```

### 设置所有者
```
chown -R root:root /usr/local/java/
```

# 配置环境变量
### 配置系统环境变量
```
nano /etc/environment
```
### 添加如下语句
```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games"
export JAVA_HOME=/usr/local/java/jdk1.8.0_152
export JRE_HOME=/usr/local/java/jdk1.8.0_152/jre
export CLASSPATH=$CLASSPATH:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
```

### 配置用户环境变量
```
nano /etc/profile
```

### 添加如下语句
```
if [ "$PS1" ]; then
  if [ "$BASH" ] && [ "$BASH" != "/bin/sh" ]; then
    # The file bash.bashrc already sets the default PS1.
    # PS1='\h:\w\$ '
    if [ -f /etc/bash.bashrc ]; then
      . /etc/bash.bashrc
    fi
  else
    if [ "`id -u`" -eq 0 ]; then
      PS1='# '
    else
      PS1='$ '
    fi
  fi
fi

export JAVA_HOME=/usr/local/java/jdk1.8.0_152
export JRE_HOME=/usr/local/java/jdk1.8.0_152/jre
export CLASSPATH=$CLASSPATH:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH:$HOME/bin

if [ -d /etc/profile.d ]; then
  for i in /etc/profile.d/*.sh; do
    if [ -r $i ]; then
      . $i
    fi
  done
  unset i
fi
```

### 使用户环境变量生效 
```
source /etc/profile
```

### 测试是否安装成功
```
root@UbuntuBase:/usr/local/java# java -version
java version "1.8.0_152"
Java(TM) SE Runtime Environment (build 1.8.0_152-b16)
Java HotSpot(TM) 64-Bit Server VM (build 25.152-b16, mixed mode)
```

### 为其他用户更新用户环境变量
```
su lusifer
source /etc/profile
```