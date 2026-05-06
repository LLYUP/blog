---
title: CSS Flexbox 布局完全指南
cover: /img/flexbox.png
categories:
  - 前端开发
tags:
  - CSS
  - Flexbox
  - 布局
abbrlink: css-flexbox-guide
date: 2026-05-06 10:00:00
description: 详细讲解 CSS Flexbox 布局模型的各项属性和用法，让你轻松掌握一维布局。
---

Flexbox 是 CSS3 引入的一种强大的一维布局模型，用它来实现各种布局既简单又高效。这篇教程带你彻底掌握 Flexbox。

---

## 一、什么是 Flexbox

Flexbox 即 Flexible Box（弹性盒子），是一种一维布局方法，适合处理页面中某一方向的布局（行或列）。

### 核心概念

- **容器（Flex Container）**：设置 `display: flex` 的元素
- **项目（Flex Items）**：容器的直接子元素
- **主轴（Main Axis）**：项目排列的方向
- **交叉轴（Cross Axis）**：垂直于主轴的方向

---

## 二、容器的属性

### 2.1 display

```css
.container {
  display: flex;    /* 块级弹性容器 */
  /* display: inline-flex;  行内弹性容器 */
}
```

### 2.2 flex-direction

设置主轴方向：

```css
.container {
  flex-direction: row;           /* 默认：左到右 */
  /* flex-direction: row-reverse;  右到左 */
  /* flex-direction: column;      上到下 */
  /* flex-direction: column-reverse; 下到上 */
}
```

### 2.3 flex-wrap

控制项目是否换行：

```css
.container {
  flex-wrap: nowrap;     /* 默认：不换行 */
  /* flex-wrap: wrap;      换行，第一行在上 */
  /* flex-wrap: wrap-reverse; 换行，第一行在下 */
}
```

### 2.4 justify-content

定义项目在主轴上的对齐方式：

```css
.container {
  justify-content: flex-start;    /* 默认：左对齐 */
  /* justify-content: flex-end;      右对齐 */
  /* justify-content: center;        居中 */
  /* justify-content: space-between; 两端对齐，项目间间隔相等 */
  /* justify-content: space-around;   项目两侧间隔相等 */
  /* justify-content: space-evenly;  项目间间隔完全相等 */
}
```

### 2.5 align-items

定义项目在交叉轴上的对齐方式：

```css
.container {
  align-items: stretch;      /* 默认：占满容器高度 */
  /* align-items: flex-start;  交叉轴起点对齐 */
  /* align-items: flex-end;    交叉轴终点对齐 */
  /* align-items: center;      交叉轴居中 */
  /* align-items: baseline;    项目基线对齐 */
}
```

### 2.6 align-content

当有多行时，定义行在交叉轴上的对齐方式：

```css
.container {
  align-content: stretch;        /* 默认 */
  /* align-content: flex-start;    交叉轴起点 */
  /* align-content: flex-end;      交叉轴终点 */
  /* align-content: center;        居中 */
  /* align-content: space-between;  两端对齐 */
  /* align-content: space-around;   两侧间隔相等 */
}
```

---

## 三、项目属性

### 3.1 flex-grow

定义项目的放大比例，默认 `0`：

```css
.item {
  flex-grow: 1;  /* 占据剩余空间的比例 */
}
```

### 3.2 flex-shrink

定义项目的缩小比例，默认 `1`：

```css
.item {
  flex-shrink: 0;  /* 0 表示不缩小 */
}
```

### 3.3 flex-basis

定义项目占据的主轴空间：

```css
.item {
  flex-basis: auto;    /* 默认：自身尺寸 */
  /* flex-basis: 200px;  固定宽度 */
}
```

### 3.4 flex（缩写）

推荐使用缩写：

```css
.item {
  flex: 1;           /* flex-grow: 1; flex-shrink: 1; flex-basis: 0%; */
  flex: 0 0 200px;    /* 不放大、不缩小、固定200px */
  flex: auto;         /* flex-grow: 1; flex-shrink: 1; flex-basis: auto; */
}
```

### 3.5 align-self

覆盖容器的 `align-items`：

```css
.item {
  align-self: center;  /* 单独设置垂直居中 */
}
```

### 3.6 order

定义项目的排列顺序：

```css
.item {
  order: -1;  /* 数值越小越靠前，默认0 */
}
```

---

## 四、实战案例

### 4.1 水平垂直居中

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

### 4.2 固定宽度 + 自适应

```css
.container {
  display: flex;
}
.sidebar {
  width: 200px;
  flex-shrink: 0;
}
.content {
  flex: 1;  /* 占据剩余空间 */
}
```

### 4.3 三栏布局

```css
.container {
  display: flex;
  justify-content: space-between;
}
.column {
  flex: 1;
}
.column:nth-child(2) {
  flex: 2;  /* 中间栏更宽 */
}
```

### 4.4 响应式导航栏

```css
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-links {
  display: flex;
  gap: 20px;
}

@media (max-width: 768px) {
  .nav {
    flex-direction: column;
    gap: 20px;
  }
}
```

---

## 五、常见问题

### 5.1 项目不换行

如果项目太多，一行排不下又不换行，项目会被压缩：

```css
.container {
  display: flex;
  flex-wrap: wrap;  /* 加这个 */
}
```

### 5.2 子元素不听话

flex 只影响直接子元素，孙元素不受影响。

### 5.3 与 margin:auto 的配合

```css
.item {
  margin-left: auto;  /* 把项目挤到右边 */
}
```

---

## 六、图解速查

```
justify-content (主轴对齐)
flex-start → ← ← ← ← ← ← ←
← → → → → → → → flex-end
← → center → ←
item  ← → item  ← → item
space-between: item  item  item
space-around:  ←item→  ←item→  ←item→
```

```
align-items (交叉轴对齐)
stretch: ████████████████████
flex-start: ██
              ██
flex-end:   ██
              ██
center:    ██
            ██
baseline:  ██ (文本对齐)
```

---

Flexbox 是现代 CSS 布局的基础，建议熟练掌握。有问题欢迎留言！
