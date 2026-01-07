---
title: "实验二：Linux开发环境搭建（超详细版）"
cover: /img/linux/cover.png
categories:
  - Linux
tags:
  - Linux
abbrlink: 25cb
date: 2025-05-29 23:27:43
---

## 🧠 实验目的

通过这次实验，你将学会以下技能：

- 使用 `yum` 安装软件包
- 下载、安装并配置 Java 开发环境（JDK）
- 使用 `vim` 编辑器编辑 Java 程序
- 使用 `git` 工具进行版本控制和上传到 Gitee
- 修改 shell 脚本并运行一个简单的贪吃蛇游戏

---

## 🌐 一、`yum` 命令简介

### 什么是 yum？

`yum`（Yellowdog Updater, Modified）是 Linux 中的包管理工具，可以用来安装、卸载、更新系统中的软件包。

### 常用命令：

| 命令 | 说明 |
|------|------|
| `yum install 软件包名` | 安装软件 |
| `yum remove 软件包名` | 卸载软件 |
| `yum update` | 更新所有软件 |
| `yum search 软件名` | 搜索软件包 |

---

## ☕️ 二、安装 JDK（Java Development Kit）

### 1. 下载 JDK 安装包

```bash
wget https://download.oracle.com/java/17/archive/jdk-17.0.12_linux-x64_bin.tar.gz
```

> 💡 `wget` 是 Linux 中用来下载文件的工具。如果没有，可以用 `yum install wget` 安装。

### 2. 解压 JDK

```bash
tar -zxvf jdk-17.0.12_linux-x64_bin.tar.gz
```

### 3. 配置环境变量

```bash
vim ~/.bash_profile
```

添加以下内容：

```bash

export JAVA_HOME=你的jdk路径
export PATH=$JAVA_HOME/bin:$PATH
```

执行：

```bash
source ~/.bash_profile
```

### 4. 验证安装是否成功

```bash
java --version
```

---

## 🧬 三、安装并使用 Git

### 1. 安装 Git

```bash
sudo yum -y install git
```

### 2. 检查安装是否成功

```bash
git --version
```

### 3. 配置用户信息

```bash
git config --global user.email "你的邮箱"
git config --global user.name "linux_学号"
```

---

## 🧱 四、Gitee 仓库的使用

### 1. 注册 Gitee 并创建仓库

访问：https://gitee.com  
点击【注册】，然后登录。

创建新仓库，名字为 `Test1`

注意一定要初始化！！！！

### 2. 克隆仓库到本地

```bash
git clone 你的仓库地址
cd Test1
```

---

## ✏️ 五、使用 Vim 编写 Java 程序

### 1. 创建并编辑 T1.java

```bash
vim T1.java
```

```java
public class T1 {
    public static void main(String[] args) {
        for (int i = 100; i < 1000; i++) {
            int a = i / 100;
            int b = (i / 10) % 10;
            int c = i % 10;
            if (a*a*a + b*b*b + c*c*c == i) {
                System.out.print(i + ",");
            }
        }
    }
}
```

### 2. 编译并运行

```bash
javac T1.java
java T1
```

### 3. 提交到 Gitee

```bash
git add T1.java
git commit -m "水仙花数"
git push
```

---

## 🧮 六、Circle 类计算周长与面积

### 1. 创建 Circle.java

```java
public class Circle {
    double r;
    public Circle(double r) {
        this.r = r;
    }

    public double getArea() {
        return Math.round(Math.PI * r * r * 100) / 100.0;
    }

    public double getPerimeter() {
        return Math.round(2 * Math.PI * r * 100) / 100.0;
    }
}
```

### 2. 创建 T2.java

```java
public class T2 {
    public static void main(String[] args) {
        Circle c = new Circle(3);
        System.out.println(c.getPerimeter() + "," + c.getArea());
    }
}
```

编译运行并提交：

```bash
javac *.java
java T2
git add .
git commit -m "圆面积和周长"
git push
```

---

## 🐍 七、贪吃蛇小游戏

### 1. 下载脚本

```bash
wget -P Test1 http://istar.kenwencs.cn/linux/snake.sh
cd Test1
chmod +x snake.sh
```

### 2. 编辑脚本内容

使用 vim 修改作者信息、删除指定行、添加函数、替换关键词等。使用命令：

- `:set number`
- `42G` / `168G` 跳转行
- `dd` 删除行
- `:%s/旧/新/g` 批量替换
- `u` 撤销操作

### 3. 提交 first 版本

```bash
git commit -m "贪吃蛇first"
git push
```

### 4. 运行并提交 second 版本

```bash
bash snake.sh
git commit -m "贪吃蛇second"
git push
```

---

## ✅ 常用命令速查表

| 命令 | 说明 |
|------|------|
| `cd` | 进入目录 |
| `ls` | 查看目录内容 |
| `pwd` | 显示当前路径 |
| `cat 文件名` | 查看文件内容 |
| `javac` | 编译 Java |
| `java` | 运行 Java |
| `vim 文件名` | 编辑文件 |

---

**完成后请保留截图并提交实验报告！**
