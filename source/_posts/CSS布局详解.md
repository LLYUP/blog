---
title: CSS布局神器：Flexbox与Grid详解
cover: /img/css-layout.png
categories:
  - 前端开发
tags:
  - CSS
  - Flexbox
  - Grid
  - 布局
abbrlink: css-flexbox-grid
date: 2026-05-05 14:00:00
description: 详细讲解CSS Flexbox和Grid两大布局模块的使用方法，通过实例帮你快速掌握现代CSS布局技巧。
---

CSS布局经历了从浮动到Flexbox再到Grid的演进。Flexbox和Grid是现代CSS布局的两大支柱，几乎可以解决所有的布局需求。本文带你彻底搞懂这两种布局方式。

---

## 一、Flexbox 弹性布局

Flexbox 是一维布局模型，适合处理一行或一列的布局。

### 1.1 基础概念

```css
.container {
  display: flex;
}
```

**核心概念**：
- **主轴（main axis）**：Flex项目排列的方向
- **交叉轴（cross axis）**：垂直于主轴的方向
- **容器的属性**：控制布局规则
- **项目的属性**：控制自身行为

### 1.2 容器属性

```css
.flex-container {
  /* 排列方向 */
  flex-direction: row | row-reverse | column | column-reverse;

  /* 是否换行 */
  flex-wrap: nowrap | wrap | wrap-reverse;

  /* 主轴对齐 */
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;

  /* 交叉轴对齐 */
  align-items: stretch | flex-start | flex-end | center | baseline;

  /* 多行对齐（需要flex-wrap: wrap） */
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

### 1.3 项目属性

```css
.flex-item {
  /* 放大比例 */
  flex-grow: 0;  /* 默认不放大 */

  /* 缩小比例 */
  flex-shrink: 1;  /* 默认可缩小 */

  /* 初始大小 */
  flex-basis: auto;

  /* 简写 */
  flex: 1;  /* 相当于 flex-grow: 1; flex-shrink: 1; flex-basis: 0%; */

  /* 单独对齐 */
  align-self: auto | flex-start | flex-end | center | stretch;
}
```

### 1.4 实战案例

**案例一：水平垂直居中**

```css
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
```

**案例二：导航栏**

```css
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
}

.nav-links {
  display: flex;
  gap: 20px;  /* 项目间距 */
}
```

**案例三：Sticky Footer（始终在底部）**

```css
.page {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.content {
  flex: 1;  /* 占据剩余空间 */
}
```

---

## 二、Grid 网格布局

Grid 是二维布局模型，同时处理行和列。

### 2.1 基础概念

```css
.container {
  display: grid;
}
```

### 2.2 定义网格

```css
.grid-container {
  /* 定义列 */
  grid-template-columns: 200px 1fr 200px;

  /* 定义行 */
  grid-template-rows: auto 1fr auto;

  /* 简写 */
  grid-template: auto 1fr auto / 200px 1fr 200px;

  /* 常用单位 */
  /* fr: 比例单位 */
  /* auto: 自动计算 */
  /* minmax(min, max): 范围 */
  /* repeat(n, value): 重复 */
}
```

### 2.3 间距

```css
.grid {
  gap: 20px;        /*行列间距相同*/
  row-gap: 10px;    /*行间距*/
  column-gap: 30px; /*列间距*/
}
```

### 2.4 定位项目

```css
.item {
  /* 指定列线 */
  grid-column: 1 / 3;      /* 从第1列线到第3列线 */
  grid-column: span 2;     /* 跨2列 */

  /* 指定行线 */
  grid-row: 1 / 3;

  /* 简写 */
  grid-area: 1 / 1 / 3 / 3;  /* row-start / col-start / row-end / col-end */
}
```

### 2.5 实战案例

**案例一：经典圣杯布局**

```css
.layout {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header header header"
    "nav main aside"
    "footer footer footer";
  min-height: 100vh;
}

.header { grid-area: header; }
.nav { grid-area: nav; }
.main { grid-area: main; }
.aside { grid-area: aside; }
.footer { grid-area: footer; }
```

**案例二：响应式卡片网格**

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
}
```

**案例三：两栏布局**

```css
.two-col {
  display: grid;
  grid-template-columns: 1fr 300px;
  gap: 40px;
}

@media (max-width: 768px) {
  .two-col {
    grid-template-columns: 1fr;
  }
}
```

---

## 三、Flexbox vs Grid 对比

| 特性 | Flexbox | Grid |
|------|---------|------|
| 维度 | 一维（行或列） | 二维（行和列） |
| 适用场景 | 导航、列表、居中 | 页面整体布局、卡片网格 |
| 分配方式 | 内容驱动 | 容器驱动 |
| 项目定位 | 按顺序 | 按网格线定位 |

## 四、配合使用

实际开发中，Flexbox 和 Grid 通常配合使用：

```css
/* Grid做整体布局 */
.page {
  display: grid;
  grid-template: auto 1fr auto / 1fr;
}

/* Flex做内部排列 */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.card-group {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}
```

---

## 五、浏览器支持

两种布局的浏览器支持都很好：

- Chrome 29+
- Firefox 28+
- Safari 9+
- Edge 16+

不需要担心兼容性问题，可以放心使用。

---

掌握Flexbox和Grid，CSS布局再也不是难题。建议两者都熟练，灵活运用才能游刃有余。

有问题欢迎留言讨论！
