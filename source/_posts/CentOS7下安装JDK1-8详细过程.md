---
title: CentOS7下安装JDK1.8详细过程
date: 2023-07-21 14:14:35
tags: jdk,centos
description: 对学习一些看法
cover: https://pics4.baidu.com/feed/d000baa1cd11728b8a7d076d725c42c2c2fd2c5e.jpeg@f_auto?token=e3a2475ddf6c76c41d4dd0ea6c349fbd
copyright: true
opyright_author: 林少鹏
---
# [CentOS7](https://so.csdn.net/so/search?q=CentOS7&spm=1001.2101.3001.7020)下安装JDK1.8详细过程

## ***1. 卸载系统自带的OpenJDK以及相关的java文件***  

1.1 查看系统是否自带JDK 

键入命令 java -version

```
java -version
```

1.2 查看相关java文件

键入命令 rpm -qa | grep java

1.3 删除相关文件

首先键入命令 su root 输入密码获取root权限，然后将上一步中带[openjdk](https://so.csdn.net/so/search?q=openjdk&spm=1001.2101.3001.7020)的文件全部删除，具体根据你安装的版本不同，文件也不尽相同，这里以上一步中的文件为例。

```sh
rpm -e --nodeps java-1.8.0-openjdk-headless-1.8.0.65-3.b17.el7.x86_64
rpm -e --nodeps java-1.8.0-openjdk-1.8.0.65-3.b17.el7.x86_64
```

1.4 查看删除结果

再次键入命令 java -version 出现以下结果表示删除成功

## **2. 下载JDK**

下载地址<http://www.oracle.com/technetwork/java/javase/downloads/index.html>

往下来拉找到jdk1.8版本的下载地址，点击下载对应的tar.gz文件

在home下的下载中找到下好的文件，此时文件所在的目录为/home/你的主机名字/下载

键入命令 cp jdk-8u211-linux-x64.tar.gz /usr/java1.8 将文件复制到/usr 下重命名为java1.8

这一步需要root权限，没有权限需要先键入命令su root 获取权限

## **3. 解压安装JDK**

键入命令 cd /usr 来到刚才的复制文件处，键入命令tar -zxvf java1.8 进行解压 解压效果如下

## **4. 配置JDK环境变量**

键入命令 vim /etc/profile 修改配置文件，记得要在root权限下修改

输入i进入编辑状态，然后将光标移到最后一行，粘贴如下内容，JAVA_HOME=/usr/jdk1.8.0_211 要根据自己的解压目录设置

```shell
#java environment
export JAVA_HOME=/usr/jdk1.8.0_211
export CLASSPATH=.:${JAVA_HOME}/jre/lib/rt.jar:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar
export PATH=$PATH:${JAVA_HOME}/bin
```

点击esc 进入命令模式 输入：wq! 保存修改信息

然后键入命令source /etc/profile 使配置文件生效

## **5. 测试安装效果**

键入命令 java -version 得到如下结果 表示安装成功