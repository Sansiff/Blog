---
title: CSAPP Lab0 Environment
date: 2024-06-04 14:51:14
categories: CSAPP
tags: CSAPP
typora-root-url: csapplab0environment
---

## 资源下载

CSAPP Lab网址：https://csapp.cs.cmu.edu/3e/labs.html

点击对应Lab后面的Self-Study Handout可以下载资源压缩包

## 环境准备

我使用的电脑是M2的Mac Mini，由于arm gcc/g++的-m编译参数中不支持32位或64位，因此选择搭建x86的Ubuntu docker来完成对实验代码的编译

拉取Ubuntu20.04镜像，创建Ubuntu(x86)容器（默认是arm架构的容器，需要指定平台为amd64）

```shell
docker pull ubuntu:20.04
docker run -it --platform linux/amd64 -v "/Users/proc/csapp:/csapp" --name=csapp ubuntu:20.04 /bin/bash
```

其中，-v "/Users/proc/csapp:/csapp" 将文件目录与容器目录进行共享以实现容器和本机的同步，这样可以在本机上写代码，docker上进行编译

安装必要的软件包

```shell
sudo apt install build-essential gcc-multilib gdb
```

在搭建好的docker容器内进入datalab目录，测试环境是否正常

```shell
make btest
./btest
```

![](EnvironmentTest.png)
能够正常运行则说明环境搭建完成

## Lab介绍

- Lab1 datalab：操作bits
- Lab2 bomblab：拆除一个二进制炸弹
- Lab3 attacklab：基本的代码注入攻击
- Lab4 cachelab：实现一个cache并且进行优化
- Lab5 tshlab：实现一个shell
- Lab6 malloclab：实现malloc和free
- Lab7 proxylab：实现一个web proxy



## 踩坑

### 编译代码时报错 gcc: error: unrecognized command line option ‘-m32’

arm版gcc不支持-m32参数，目前没有合理的解决方案，最终选择搭建x86的Ubuntu来完成代码的编译工作

### docker拉取软件包的速度过慢

选择换源为国内的镜像源，更改位置在/etc/apt/sources.list 

首先将原来的文件进行备份，更换其中内容后重新update即可

```shell
cp /etc/apt/sources.list /etc/apt/sources.list.bak
modify /etc/apt/sources.list 
sudo apt-get update
```