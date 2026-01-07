---
title: Git 使用教程（以 CentOS 7 + Gitee 为例）
cover: /img/git.png
categories:
  - git
tags:
  - git
abbrlink: 6b8e
date: 2025-05-30 11:10:43
---

本教程以 CentOS 7 系统为基础，结合 [Gitee](https://gitee.com/) 平台，详细介绍 Git 的安装、配置、基本使用及常见操作。适合初学者快速上手 Git。

------

## 📆 一、安装 Git（CentOS 7）

打开终端，执行以下命令安装 Git：

```bash
sudo yum update -y
sudo yum install git -y
```

检查版本：

```bash
git --version
```

> 若输出 `git version x.x.x`，说明安装成功。

------

## 🧰 二、配置 Git 用户信息

首次使用 Git 时，需要配置用户信息：

```bash
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```

查看配置信息：

```bash
git config --list
```

------

## 🛠️ 三、注册 Gitee 并创建仓库

### 1. 注册账号

访问 [https://gitee.com](https://gitee.com/)，注册并登录。

### 2. 创建仓库

- 登录后点击右上角 “+” → “新建仓库”
- 填写仓库名（如：`my-first-project`）
- 可选勾选 “初始化仓库”（推荐）
- 点击 “创建”

------

## 🔐 四、配置 SSH 密钥（推荐方式）

### 1. 生成 SSH 密钥

```bash
ssh-keygen -t rsa -C "你的邮箱"
```

一路回车默认即可，会在 `~/.ssh/id_rsa.pub` 生成公钥。

### 2. 查看并复制公钥内容

```bash
cat ~/.ssh/id_rsa.pub
```

### 3. 添加到 Gitee

- 登录 Gitee → 点击头像 → 设置 → 安全设置 → SSH 公钥
- 点“添加 SSH 公钥”，粘贴上步复制的内容，保存

### 4. 测试连接

```bash
ssh -T git@gitee.com
```

首次连接会提示 yes/no，输入 `yes`，若看到欢迎信息则配置成功。

------

## 📁 五、克隆仓库到本地

### 1. 复制仓库地址（SSH）

在仓库页面，点击 “克隆/ 下载” → 选择 SSH → 复制地址，如：

```
git@gitee.com:your_username/my-first-project.git
```

### 2. 克隆仓库

```bash
git clone git@gitee.com:your_username/my-first-project.git
```

------

## ✍️ 六、基本使用流程

### 1. 进入仓库目录

```bash
cd my-first-project
```

### 2. 编辑/添加文件

```bash
echo "# 我的第一个项目" > README.md
```

### 3. 添加到暂存区

```bash
git add README.md
```

或者全部添加：

```bash
git add .
```

### 4. 提交到本地仓库

```bash
git commit -m "说明"
```

### 5. 推送到远程仓库

```bash
git push origin master
```

------

## 🔀 七、常用 Git 命令总结

| 功能         | 命令                             |
| ------------ | -------------------------------- |
| 克隆仓库     | `git clone 仓库地址`             |
| 查看状态     | `git status`                     |
| 添加更改     | `git add 文件名` 或 `git add .`  |
| 提交更改     | `git commit -m "描述"`           |
| 推送到远程   | `git push origin 分支名`         |
| 拉取远程更新 | `git pull`                       |
| 查看日志     | `git log` 或 `git log --oneline` |
| 创建分支     | `git checkout -b 分支名`         |
| 切换分支     | `git checkout 分支名`            |
| 合并分支     | `git merge 分支名`               |

------

## 💡 八、问题排查

### 【问题】提交时报错“Please tell me who you are”

**解决：** 未配置用户名和邮箱

```bash
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```

### 【问题】 SSH 连接失败

- 检查 `~/.ssh/id_rsa.pub` 是否存在
- 使用 `ssh -T git@gitee.com` 测试
- 确保公钥已添加到 Gitee

------

## 📚 九、推荐学习资源

- Gitee 官方文档：https://gitee.com/help
- 廖雪峰 Git 教程：https://www.liaoxuefeng.com/wiki/896043488029600
- Pro Git 中文版：https://git-scm.com/book/zh/v2

------

> 🎉 到此为止，你已经掌握了在 CentOS 7 系统中配合 Gitee 管理代码的基本流程，加油！