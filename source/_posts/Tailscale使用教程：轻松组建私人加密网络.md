---
title: Tailscale 使用教程：轻松组建私人加密网络
cover: /img/tailscale.png
categories:
  - 工具教程
tags:
  - Tailscale
  - VPN
  - 网络
abbrlink: 7f3a
date: 2026-05-28 12:10:00
---

Tailscale 是一款基于 WireGuard 的零配置 VPN 网络工具，能够让你轻松安全地连接任意设备，无需手动配置防火墙或端口转发。本文详细介绍 Tailscale 的安装、配置与常见使用场景。

<!-- more -->

------

## 📆 一、什么是 Tailscale？

Tailscale 利用 WireGuard 协议实现设备间的点对点加密连接，支持 NAT 穿透，设备之间可以直接通信，无需中转服务器。这让它比传统 VPN 更快、更安全、更易用。

### 核心特性

- 🔒 **端到端加密** — 基于 WireGuard，流量全程加密
- 🌐 **零配置组网** — 无需公网服务器或复杂配置
- 🔄 **NAT 穿透** — 自动打洞，畅快互联
- 👥 **设备管理** — Web 控制台统一管理所有设备
- 🚀 **多平台支持** — Windows、macOS、Linux、iOS、Android、Synology、QNAP 等

------

## 📆 二、安装与登录

### 1. 注册账号

访问 [tailscale.com](https://login.tailscale.com)，使用 GitHub、Google 或微软账号登录。

### 2. 下载客户端

| 平台 | 安装方式 |
|------|----------|
| macOS | `brew install tailscale` 或[官网下载](https://pkgs.tailscale.com/stable/) |
| Windows | [官网下载](https://pkgs.tailscale.com/stable/)安装包 |
| Linux | `curl -fsSL https://tailscale.com/install.sh \| sh` |
| iOS | App Store 搜索 "Tailscale" |
| Android | Google Play 或应用商店搜索 "Tailscale" |

### 3. 登录连接

```bash
# Linux/macOS 终端
sudo tailscale up

# Windows / macOS GUI 版本
# 点击 "Log in" 按钮，浏览器自动弹出授权页面
```

浏览器弹出授权页面，确认后设备即接入网络。

------

## 📆 三、基础命令

```bash
# 查看当前状态和所有设备
tailscale status

# 查看本机 Tailscale IP
tailscale ip

# 断开连接
sudo tailscale down

# 重新连接
sudo tailscale up

# 查看所有设备详细信息
tailscale status --json | jq '.Peer'
```

------

## 📆 四、进阶配置

### 1. 启用 SSH 远程访问

```bash
sudo tailscale up --ssh
```

开启后即可直接通过 `tailscale ssh user@hostname` 连接目标设备，即使目标在 NAT 后面。

### 2. 子网路由（Subnet Router）

将 Tailscale 网络流量转发到物理子网，例如访问家庭内网：

```bash
# 在 Linux 网关设备上运行
sudo tailscale up --advertise-routes=192.168.1.0/24

# 前往 https://login.tailscale.com/1/acls
# 在 ACL 中添加策略允许流量通行
```

### 3. 自定义 DERP 中继

Tailscale 默认使用公共 DERP 服务器，必要时可配置自建中继：

```bash
sudo tailscale up --derp-map=https://your-derp-server.com/map
```

### 4. 禁用 IPv6

某些环境下 IPv6 可能干扰 Tailscale 流量：

```bash
sudo tailscale up --accept-routes=false
```

------

## 📆 五、ACL 访问控制

访问 [ACL 页面](https://login.tailscale.com/1/acls) 编辑 JSON 策略，精细控制设备间的访问权限：

```json
{
  "acls": [
    {
      "action": "accept",
      "src": ["autogroup:members"],
      "dst": ["autogroup:members:*"]
    }
  ],
  "ssh": [
    {
      "action": "accept",
      "src": ["autogroup:members"],
      "dst": ["autogroup:self"],
      "users": ["autogroup:nonroot"]
    }
  ]
}
```

------

## 📆 六、常见使用场景

### 🏠 家庭网络
不在家也能访问家里 NAS、树莓派、智能家居设备，无需暴露公网端口。

### 🖥️ 远程办公
安全访问公司内网资源，无需传统 VPN 的复杂配置。

### 🧪 开发测试
连接多台服务器进行调试，像在同一个局域网内一样操作。

### 📁 文件共享
通过 Tailscale 网络直接 SMB/NFS 传输文件，无需公网暴露。

------

## 📆 七、常见问题

**Q: Tailscale 与传统 VPN 有什么区别？**

传统 VPN 流量必须经过中转服务器，延迟高、带宽受限。Tailscale 基于 WireGuard，支持 NAT 穿透直连，延迟更低，速度更快。

**Q: 免费版支持多少台设备？**

个人用户免费版最多支持 100 台设备，足够个人和小型团队使用。

**Q: Tailscale 服务器能看到我的流量吗？**

不能。Tailscale 使用 WireGuard 端到端加密，服务端只负责握手，无法解密流量内容。

**Q: 如何撤销某台设备的访问权限？**

在 [管理面板](https://login.tailscale.com/admin/machines) 中找到对应设备，点击 "Edit" → "Logout" 即可撤销。

------

## 📆 八、相关资源

- 📖 官方文档：https://tailscale.com/kb/
- 💻 GitHub：https://github.com/tailscale/tailscale
- 📋 官方博客：https://tailscale.com/blog/

如果你有任何问题，欢迎在评论区留言交流！

> 本文使用 Tailscale v1.70+ 编写，不同版本界面可能略有差异。
