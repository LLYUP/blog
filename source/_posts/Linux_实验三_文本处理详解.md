---
title: "实验三：Linux文本处理（超详细版）"
cover: /img/linux/cover.png
categories:
  - Linux
tags:
  - Linux
abbrlink: '0'
date: 2025-05-30 10:32:43
---

## 🧠 实验目的

掌握 Linux 中文本处理的基本操作，包括：

- 使用 `wget` 下载文件
- 使用 `sort`、`uniq`、`grep`、`cut`、`head`、`awk` 等命令处理文本
- 编写简单的 Shell 脚本
- 使用 Git 管理并提交实验结果

---

## 🧰 实验准备

- 一台联网的 Linux 电脑
- 安装了常用命令（如 `wget`, `sort`, `uniq`, `grep`, `cut`, `awk`, `git` 等）
- 熟悉 Gitee 仓库操作（见实验二）
- 确保你已经有本地的 `Test1` 仓库（`git clone` 下来的）

---

## 📦 一、下载原始数据文件

```bash
wget http://istar.kenwencs.cn/linux/metals_random.txt
ls
```

---

## 🔤 二、国家拼音排序、去重、重定向保存

```bash
LC_ALL=zh_CN.UTF-8 sort -u metals_random.txt > metals.txt
```

**注意事项**：

1. 确保系统已安装中文语言包（如未安装需先执行）：

   ```bash
   sudo yum install -y glibc-common zh_CN*
   sudo localedef -c -f UTF-8 -i zh_CN zh_CN.UTF-8
   ```

2. 若原始文件编码非UTF-8，需先转换编码：

   ```bash
   iconv -f GBK -t UTF-8 metals_random.txt > metals_utf8.txt
   ```

---

## 📁 三、移动 metals.txt 到 Test1 并提交到 Gitee

```bash
mv metals.txt Test1/
cd Test1
git add metals.txt
git commit -m "巴黎奥运会奖牌榜"
git push
```

---

## 🧮 四、统计国家总数

```bash
awk -F, '{ country = $1;print country;}' metals.txt | sort | uniq | wc -l
```

将命令写入脚本

```bash
vim myshell1.sh
将命令写入脚本保存
```

上传到gitee

```bash
git add myshell1.sh
git commit -m "巴黎奥运会获奖数"
git push
```

---

## 🇨🇳 五、筛选中国三地并按奖牌总数降序排列

```bash
grep -E '中国,|中国台北,|中国香港,' metals.txt | sort -t',' -k2,2nr -k3,3nr -k4,4nr
```

将命令写入脚本后上传至gitee(同上)

```bash
git add myshell1.sh
git commit -m "巴黎奥运会中国奖牌榜"
git push
```

---

## 🥉 六、筛选铜牌前五名国家（仅输出国家名）

```bash
sort -t',' -k4nr metals.txt | head -n 5 | cut -d',' -f1
```

将命令写入脚本后上传至gitee(同上)

```bash
git add myshell1.sh
git commit -m "铜牌前五的国家"
git push
```

---

## 🥇 七、统计金牌前五的金牌总数

```bash
sort -t, -k2 -nr metals.txt | head -n 5 | tee >(awk -F, '{sum += $2} END {print "" sum}')
```

将命令写入脚本后上传至gitee(同上)

```bash
git add myshell1.sh
git commit -m "巴黎奥运会金牌前五的金牌总数"
git push
```

---

## ✅ 脚本最终内容示例（myshell1.sh）

```bash
awk -F, '{ country = $1;print country;}' metals.txt | sort | uniq | wc -l
grep -E '中国,|中国台北,|中国香港,' metals.txt | sort -t',' -k2,2nr -k3,3nr -k4,4nr
sort -t',' -k4nr metals.txt | head -n 5 | cut -d',' -f1
sort -t, -k2 -nr metals.txt | head -n 5 | tee >(awk -F, '{sum += $2} END {print "" sum}')
```

---

## 📌 附录：常用命令解释

| 命令 | 说明 |
|------|------|
| `wget URL` | 下载文件 |
| `sort` | 排序文本 |
| `grep` | 匹配关键字 |
| `cut` | 提取指定列 |
| `awk` | 行列处理与计算 |
| `head` | 显示前几行 |
| `mv` | 移动文件 |
| `git add` | 添加修改文件 |
| `git commit -m "说明"` | 提交修改 |
| `git push` | 上传到 Gitee |
