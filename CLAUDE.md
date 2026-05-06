# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hexo blog named "墨问" (http://blog.llystar.cn) — a Chinese-language blog about product design, development, and translations. Uses the anzhiyu theme variant.

## Common Commands

```bash
hexo server      # Start dev server (http://localhost:4000)
hexo generate    # Build static files to public/
hexo clean       # Clear cache and generated files
hexo deploy      # Deploy to production
```

## Architecture

- **source/_posts/** — Markdown blog posts (Chinese content)
- **themes/anzhiyu/** — Butterfly theme variant with custom config in `_config.anzhiyu.yml`
- **scaffolds/** — Post/page draft templates for new content
- **source/** — Static content organized by type (about, categories, tags, essays, etc.)

## Key Configurations

- **permalink:** `posts/:abbrlink/` — Uses crc16+hex algorithm for URL slugs
- **Plugins:** mathjax (LaTeX), envelope_comment (message board), abbrlink, wordcount, search
- **Renderers:** marked (Markdown), ejs, pug, stylus
- **Language:** zh-CN with Asia/Shanghai timezone
- **Comments:** Twikoo (https://twikoo.llystar.cn/)
- **Social:** GitHub, Bilibili, RSS
- **RSS:** /atom.xml
- **Menu items:** 文章(归档/分类/标签), 友链(友人帐/朋友圈/留言板), 我的(音乐馆/小空调), 关于(关于本人/闲言碎语/随便逛逛)

## Enabled Features

- **canvas_nest** — 蓝色线条背景动画
- **activate_power_mode** — 打字粒子特效
- **footer.subTitle** — 一言网打字机效果
- **wordcount** — 字数统计和阅读时间
- **reward** — 打赏功能（微信/支付宝）
- **related_post** — 相关文章推荐
- **local_search** — 本地搜索
- **card_announcement** — 博客公告栏
- **preloader** — 页面加载进度条 (pace主题)
- **sitemap** — /sitemap.xml 和 /baidusitemap.xml (SEO)

## Article Front-matter Template

```yaml
---
title: {{ title }}
date: {{ date }}
categories:
  - xxx
tags:
  - xxx
abbrlink: xxx
cover: /img/xxx.jpg
---
```
