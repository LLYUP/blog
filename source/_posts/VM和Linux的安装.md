---
title: VM和Linux的安装
cover: /img/linux/cover.png
categories:
  - Linux
tags:
  - Linux
  - VM
abbrlink: 772b
date: 2025-05-20 22:17:43
---

# 一、准备工作

## 1、VMware安装

### 1.1 下载地址

[官方网站](https://www.vmware.com/)

## 2、镜像下载

### 2.1、官方网站

### https://www.centos.org/ (官网的下载速度会很慢，不推荐）

### 2.2、其他镜像源的下载地址（推荐）

[阿里云开源镜像站](https://mirrors.aliyun.com/centos-vault/centos/)

[南阳理工学院开源镜像站](https://mirror.nyist.edu.cn/centos-vault/centos/)

## 3、选择合适版本的镜像进行下载

这里我选择centos 7.6

![1](\img\linux\1.png)

#  二、VMware新建适配虚拟机

1、打开我们的虚拟机（VMware Workstation）,点击文件进行新建

![2](\img\linux\2.png)

2、选择典型之后，下一步

![3](\img\linux\3.png)

3、选择稍会安装操作系统

![4](\img\linux\4.png)

4、因为安装的是Linux操作，我们勾选Linux，并且选择我们的CentOS 7的版本

![5](\img\linux\5.png)

5、设定我们虚拟机的名称和安装位置

![6](\img\linux\6.png)

6、指定我们虚拟机的磁盘容量大小

![7](\img\linux\7.png)

7、这里可以选择自定义硬件，或者先完成基本安装后选择编辑虚拟机

![8](\img\linux\8.png)

8、编辑虚拟机内存配置

![9](\img\linux\9.png)

9、选择我们环境的处理器数量（我选默认）

![10](\img\linux\10.png)

10、选择我们的镜像

![11](\img\linux\11.png)

11、选择网络适配器

![12](\img\linux\12.png)

# 三、配置环境

1、环境安装完之后，打开虚拟机

![13](\img\linux\13.png)

2、直接install CentOS 7

![14](\img\linux\14.png)

3、等待安装完之后，选择语言

![15](\img\linux\15.png)

4、安装信息摘要，这里本地化的三个都不需要管，直接默认；主要是软件和系统需要修改

![16](\img\linux\16.png)

5、软件安装，如果你是已经很熟悉的可以直接最小化安装，但是初学者建议选择带图形化的系统安装，同时选择开发工具

![17](\img\linux\17.png)

6、系统这里设置，我们先点击安装位置

![18](\img\linux\18.png)

7、安装位置设置之后，选择我要分区，点击完成

![19](\img\linux\19.png)

8、设置分区，点击下面的 “ + ” 号，进行设置

![20](\img\linux\20.png)

9、添加新的挂载点。/boot；swap；/

![21](\img\linux\21.png)

![22](\img\linux\22.png)

![23](\img\linux\23.png)

10、创建完挂载点之后点击完成，并接受更改

![24](\img\linux\24.png)

11、关闭kdump

![25](\img\linux\25.png)

12、网络配置

![26](\img\linux\26.png)

主机名称可以不改

后续的ip设置可以直接自动

13.安全策略选择默认就行，这就是安装之前的准备工作，下面可以开始安装了

![27](\img\linux\27.png)

14、开始安装时需要设置root账号以及用户账号，这里设置的密码如果过于简单需要重复确认一下

![28](\img\linux\28.png)

15、点击重启即可，到这里安装就是完成

![29](\img\linux\29.png)

16、安装成功界面截图

![30](\img\linux\30.png)

# 四、基础检查

查看是否可以ping通网络

![31](\img\linux\31.png)

好了，以上就是基础的Linux安装教程，谢谢大家的观看，有问题多多交流
