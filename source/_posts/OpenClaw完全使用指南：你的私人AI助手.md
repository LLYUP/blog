---
title: OpenClaw完全使用指南：把你的聊天App变成AI超级助手
cover: /img/openclaw-guide.jpg
categories:
  - AI
tags:
  - OpenClaw
  - AI助手
  - 工具
  - 自动化
abbrlink: openclaw-complete-guide
date: 2026-05-26 22:30:00
---

## 前言

想象一下：你在微信、Telegram、WhatsApp 或者 Discord 上随便发一条消息，你的私人 AI 助手就能帮你查资料、发邮件、管理日历、写代码、搜索网页——而且它 24 小时在线，永不疲倦。

这就是 **OpenClaw** 正在做的事。

OpenClaw 是一个开源的、多通道的 AI 网关。它把各种聊天应用和 AI 助手连接在一起，让你用任何一个日常聊天工具，就能驱动一个功能强大的 AI 代理为你工作。它不需要你放弃对自己数据的控制——它是自托管的，运行在你自己的机器上。

本文将详细介绍如何安装、配置和使用 OpenClaw，让它成为你真正的数字伙伴。

<!-- more -->

## OpenClaw 是什么？

OpenClaw 是一个**自托管的 AI 网关**（Self-hosted Gateway）。它是一个轻量级的服务进程，可以运行在 macOS、Linux 或 Windows（通过 WSL2）中，通过 WebSocket 连接到 AI 模型，同时对接各种聊天渠道。

用一张图来理解它的架构：

```
聊天应用（Discord / Telegram / 微信 / WhatsApp / ...）
        ↓
   OpenClaw Gateway  ← 这是核心
        ↓
   AI 助手（Claude / GPT / 本地模型...）
```

### OpenClaw 能做什么？

- **多渠道消息收发**：一个 Gateway 同时接入 Discord、Telegram、WhatsApp、Signal、Slack、飞书、微信等多个聊天平台
- **AI 助手能力**：内置工具调用、代码执行、文件管理、搜索、记忆等
- **定时任务**：设置定期提醒、自动执行的后台任务
- **多端同步**：支持桌面端、移动端（iOS/Android）配对，实现画布、摄像头、语音等能力
- **记忆系统**：跨会话的长期记忆，记住你的偏好和习惯
- **完全自托管**：数据留在你自己的机器上，不依赖任何第三方服务

### 谁适合用 OpenClaw？

- **开发者**：需要一个 24 小时在线的编程助手，可以帮你写代码、跑测试、修 Bug
- **效率党**：想把日常琐事（查资料、发提醒、管文件）交给 AI 处理
- **技术爱好者**：喜欢折腾、追求数据和隐私控制在自己手里
- **小团队**：需要一个共享的 AI 助手，通过 Slack 或飞书等平台全员使用

## 安装 OpenClaw

### 环境要求

- **Node.js**：推荐 Node 24，最低支持 Node 22 LTS（`22.19+`）
- **操作系统**：macOS、Linux（推荐）、Windows（通过 WSL2）
- **磁盘空间**：约 200MB 基础占用
- **网络**：需要访问你所用 AI 模型的 API

### 安装步骤

通过 npm 全局安装（推荐）：

```bash
npm install -g openclaw@latest
```

安装完成后，验证版本：

```bash
openclaw --version
```

## 初始化配置

OpenClaw 提供交互式引导安装，输入以下命令启动：

```bash
openclaw onboard --install-daemon
```

### 选择模式

引导过程会让你选择**快速开始**或**高级模式**：

| 模式 | 说明 |
|------|------|
| 快速开始 | 自动选择默认配置，适合大多数用户 |
| 高级模式 | 让你配置每一个细节（端口、认证方式、渠道等）|

### 配置 AI 模型

在引导过程中，你需要选择 AI 模型提供商。OpenClaw 支持：

- **OpenAI**（GPT-4、GPT-4o 等）
- **Anthropic**（Claude 系列，推荐）
- **Google Gemini**
- **本地模型**（通过 OpenAI 兼容接口）
- **自定义提供商**（OpenAI 兼容 / Anthropic 兼容 / 自动检测）

### 选择聊天渠道

OpenClaw 支持的渠道包括：

**内置渠道：**
- Discord
- Telegram
- WhatsApp
- Signal
- Slack
- 飞书（Feishu）
- 企业微信
- QQ Bot
- iMessage（macOS）

**插件渠道：**
- Google Chat
- Microsoft Teams
- Matrix
- Nostr
- Twitch
- Zalo

每个渠道的配置方式各不相同，通常需要到对应的平台开发者后台创建 Bot 或应用，获取 API Key 或 Token，然后在引导中填入。

### 守护进程安装

添加 `--install-daemon` 参数后，OpenClaw 会在系统启动时自动运行：

- **macOS**：创建 LaunchAgent
- **Linux/WSL2**：创建 systemd 用户单元
- **Windows**：创建计划任务

安装完成后，Gateway 会在后台运行，你无需手动启动。

## 核心概念

在深入使用前，需要理解几个核心概念：

### Gateway（网关）

Gateway 是 OpenClaw 的核心进程。它是一个持续运行的本地服务，监听消息并转发给 AI 模型，同时管理渠道连接、会话状态和定时任务。

### Agent（代理）

Agent 是 AI 模型的运行时实例。每个 Agent 有自己独立的：
- 工作目录（workspace）
- 会话历史
- 身份设定（SOUL.md、IDENTITY.md 等）
- 记忆文件

你可以创建多个 Agent，分别用于不同用途——比如一个写代码，一个处理邮件，一个管理日程。

### Session（会话）

每一次你和 Agent 的对话构成一个 Session。Session 可以是：
- **DM Session**：私聊会话，加载长期记忆
- **Channel Session**：群组会话，不加载个人记忆
- **Isolated Session**：隔离会话，用于定时任务等后台工作

### Skills（技能）

Skills 是 OpenClaw 的扩展模块。它们定义了 Agent 可以调用的工具集，比如：

- `searxng` — 网页搜索
- `lark-*` — 飞书系列工具
- `wecom-*` — 企业微信工具
- `weather` — 天气查询
- `memory_search` — 记忆搜索
- 等等……

你也可以自己编写 Skill，封装任意功能。

### Memory（记忆）

OpenClaw 的记忆系统由三个文件组成：

| 文件 | 用途 |
|------|------|
| `MEMORY.md` | 长期记忆：持久化的事实、偏好、决策 |
| `memory/YYYY-MM-DD.md` | 每日笔记：日常观察和上下文 |
| `DREAMS.md` | 梦境日记：自动生成的反思和回顾 |

Memory 的工作逻辑很简单：**只写入磁盘的内容才会被记住**。每次新会话开始时，Agent 会自动加载长期记忆和近期的每日笔记。

如果想告诉 Agent 一些事，直接说"记住我偏好 TypeScript"——它会自动写入记忆文件。

## 使用 Control UI

OpenClaw 提供了一个浏览器端控制面板，称为 **Control UI**。

### 访问方式

Gateway 本地运行时，打开浏览器访问：

```
http://127.0.0.1:18789/
```

或

```
http://localhost:18789/
```

### 首次配对

在新浏览器或设备上首次访问时，Gateway 会要求配对审批：

1. 浏览器显示：`disconnected (1008): pairing required`
2. 在终端运行：`openclaw devices list`（查看待审批请求）
3. 复制请求 ID，运行：`openclaw devices approve <requestId>`
4. 刷新浏览器页面完成连接

> **提示**：本地回环地址（127.0.0.1 / localhost）连接会自动批准，无需手动配对。

### Control UI 能做什么

- 聊天界面：发送消息，查看历史
- 活动面板：查看最近操作和工具调用
- 节点管理：管理配对的移动设备
- 配置面板：调整 Gateway 设置
- 主题定制：切换深色/浅色主题，支持自定义主题导入

## 多渠道接入

OpenClaw 的强大之处在于一个 Gateway 可以同时连接多个聊天平台。以下是几个常用渠道的配置要点：

### Telegram Bot

1. 在 Telegram 创建 Bot：找 `@BotFather`，发送 `/newbot`
2. 获取 Bot Token
3. 引导中选择 Telegram 渠道，填入 Token
4. 设置允许的用户 ID（安全起见，默认仅白名单用户可用）

之后在 Telegram 搜索你的 Bot 用户名，直接发消息即可。

### Discord

1. 在 Discord Developer Portal 创建 Application
2. 添加 Bot，获取 Token
3. 启用 Message Content Intent
4. 将 Bot 加入你的 Discord Server
5. 在引导中填入 Token，选择允许的频道

### 飞书（Feishu）

1. 在飞书开放平台创建企业自建应用
2. 获取 App ID 和 App Secret
3. 配置机器人能力
4. 在引导中配置飞书渠道

### 微信（通过 openclaw-weixin）

通过企业微信或个人微信通道接入，需要在引导中按提示完成 OAuth 授权流程。

## 定时任务与自动化

OpenClaw 内置了强大的定时任务系统，可以设置一次性的提醒或周期性的自动化任务。

### 创建一次性提醒

```bash
openclaw cron add \
  --name "会议提醒" \
  --at "2026-05-27T09:00:00+08:00" \
  --session main \
  --system-event "会议将在30分钟后开始" \
  --delete-after-run
```

### 创建周期性任务

```bash
openclaw cron add \
  --name "每日简报" \
  --cron "0 8 * * *" \
  --tz "Asia/Shanghai" \
  --session main \
  --system-event "发送今日新闻简报"
```

### 定时任务参数说明

| 参数 | 说明 |
|------|------|
| `--at` | 一次性任务，ISO 8601 时间戳或相对时间（如 `20m`）|
| `--every` | 固定间隔，如 `1h`、`30m` |
| `--cron` | 标准 Cron 表达式 |
| `--tz` | 时区，默认 UTC |
| `--delete-after-run` | 执行后自动删除 |
| `--session` | 指定运行的会话名称 |

查看任务列表：

```bash
openclaw cron list
```

查看任务详情：

```bash
openclaw cron get <job-id>
```

## 移动端节点配对

OpenClaw 支持将 iOS 或 Android 设备配对为节点，获得额外的设备能力：

### 可以做什么

- **画布（Canvas）**：设备屏幕共享，让 AI 看到你的屏幕
- **摄像头**：让 AI 通过摄像头观察世界
- **语音**：语音交互
- **通知推送**：设备通知推送到 Gateway

### 配对步骤

1. 安装 OpenClaw 的移动端 App（iOS 通过 TestFlight 或 App Store，Android 通过 APK）
2. 在 App 中输入 Gateway 地址和 Token
3. 在 Gateway 端审批配对请求：

```bash
openclaw devices list
openclaw devices approve <requestId>
```

### 远程节点

如果你想让 Gateway 在一台机器上运行，但命令实际在另一台机器上执行，可以使用远程节点功能：

```bash
# 在要执行命令的机器上
openclaw node run --host <gateway-host> --port 18789 --display-name "Build Node"
```

## 记忆系统详解

OpenClaw 的记忆系统是它区别于普通聊天机器人的关键。

### 长期记忆（MEMORY.md）

长期记忆文件会在每次私聊会话开始时自动加载。建议写入：
- 你的姓名、职业、时区
- 工作习惯和偏好
- 重要的项目背景和决策
- 常用的技术栈和工具

### 每日笔记（memory/YYYY-MM-DD.md）

详细的日常记录，不自动注入上下文，但可以被搜索到。建议记录：
- 当天的工作进展
- 遇到的问题和解决方案
- 有趣的想法或发现

### 如何让 Agent 记住事情

最简单的方式就是直接说：

> "记住我目前在做 X 项目，技术栈是 Y"

Agent 会自动判断这条信息应该写入哪个文件。

### 记忆搜索

如果想查找之前的记录，可以让 Agent 调用：

```
"搜索一下我之前关于 Z 的讨论"
```

它会通过语义搜索找到相关内容。

## 编写自定义 Skill

如果你需要封装一些自定义工具，可以编写 OpenClaw Skill。

### Skill 结构

一个 Skill 目录通常包含：

```
my-skill/
├── SKILL.md          # Skill 的定义文件
├── scripts/          # 脚本目录
│   └── skill.js      # 具体实现
└── references/       # 参考文档（可选）
```

### SKILL.md 示例

```markdown
---
name: my-skill
description: 做某事的技能
author: Your Name
version: 1.0.0
---

# My Skill

## Commands

### do-something
执行某项操作。

Usage: `do-something --param <value>`
```

### 在引导中安装

```bash
openclaw skills install ./my-skill
```

## 进阶配置

### 通过 Tailscale 远程访问

如果你的 Gateway 在家里运行，但你想在公司或外出时访问，可以借助 Tailscale：

```bash
openclaw configure
# 选择 Tailscale 曝光选项为 "On"
```

Tailscale 会自动建立加密隧道，无需配置端口转发或 VPN。

### 调整模型参数

```bash
openclaw config set agents.defaults.model "claude-sonnet-4-20250514"
openclaw config set agents.defaults.maxTokens 8192
```

### 设置代理

如果网络环境需要代理：

```bash
export HTTP_PROXY=http://127.0.0.1:7890
export HTTPS_PROXY=http://127.0.0.1:7890
openclaw gateway
```

## 安全建议

1. **API Key 安全**：尽量使用环境变量引用而非明文存储
2. **渠道白名单**：Telegram、WhatsApp 等默认仅白名单用户可用
3. **定期更新**：保持 OpenClaw 为最新版本，及时修复安全漏洞
4. **最小权限**：为不同 Agent 配置不同的工具权限
5. **敏感操作确认**：涉及外部操作（发邮件、支付等）建议开启确认流程

## 常见问题

**Q：Gateway 启动后显示 ` pairing required`？**

A：这是新设备的配对安全机制。在终端运行 `openclaw devices approve <requestId>` 审批即可。

**Q：消息发出去没有反应？**

A：检查 Gateway 是否正常运行：`openclaw status`。同时检查渠道是否正确连接。

**Q：如何查看详细日志？**

A：`openclaw doctor` 可以运行完整诊断。`openclaw gateway --verbose` 可以查看实时日志。

**Q：能否同时使用多个 AI 提供商？**

A：可以。你可以为不同的 Agent 指定不同的模型，也可以在同一个会话中按需切换。

**Q：记忆文件存放在哪里？**

A：默认在 `~/.openclaw/workspace/` 目录下，包括 MEMORY.md、memory/ 等。

**Q：定时任务没执行？**

A：运行 `openclaw cron list` 检查任务是否在列表中，`openclaw cron runs <job-id>` 查看执行历史。

## 总结

OpenClaw 不仅仅是一个聊天 Bot 框架，它是一个**个人 AI 基础设施**。它的核心理念是：

> **你的 AI 助手应该像你一样工作——在你常用的工具里、用你习惯的方式、记住你关心的事、执行你交代的任务。**

通过自托管的方式，OpenClaw 确保你对数据和隐私的完全控制。通过多渠道接入，它消除了在不同 App 间切换的割裂感。通过记忆系统和定时任务，它从"问答工具"进化成了真正的"数字伙伴"。

如果你还没有尝试过 OpenClaw，建议从一次本地安装开始——只需要十分钟，你就能拥有一个 24 小时在线、永不疲倦的 AI 助手。

---

**相关链接：**

- OpenClaw 官网：https://openclaw.ai
- OpenClaw 文档：https://docs.openclaw.ai
- GitHub 仓库：https://github.com/openclaw/openclaw
