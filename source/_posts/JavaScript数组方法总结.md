---
title: JavaScript 数组方法完全指南
cover: /img/js-array.png
categories:
  - 前端开发
tags:
  - JavaScript
  - ES6
  - 数组
abbrlink: js-array-methods
date: 2026-05-05 14:00:00
description: 全面总结 JavaScript 数组的各种方法，包括遍历、筛选、转换、归约等操作，配有实际例子。
---

JavaScript 数组方法是日常开发中最常用的 API 之一。这篇文章帮你系统梳理所有常用的数组方法。

---

## 一、遍历类

### 1.1 forEach

遍历数组，对每个元素执行回调：

```javascript
const arr = [1, 2, 3];

arr.forEach((item, index) => {
  console.log(`${index}: ${item}`);
});
// 0: 1
// 1: 2
// 2: 3
```

**特点**：没有返回值，不改变原数组。

### 1.2 map

创建新数组，包含每次函数调用的结果：

```javascript
const arr = [1, 2, 3];

const doubled = arr.map(item => item * 2);
console.log(doubled); // [2, 4, 6]
console.log(arr);     // [1, 2, 3] 原数组不变
```

### 1.3 for...of

ES6 引入的遍历方式：

```javascript
const arr = ['a', 'b', 'c'];

for (const item of arr) {
  console.log(item);
}
```

---

## 二、筛选类

### 2.1 filter

创建新数组，包含通过测试的元素：

```javascript
const arr = [1, 2, 3, 4, 5, 6];

const even = arr.filter(item => item % 2 === 0);
console.log(even); // [2, 4, 6]
```

### 2.2 find

返回第一个通过测试的元素：

```javascript
const users = [
  { name: '张三', age: 18 },
  { name: '李四', age: 20 },
  { name: '王五', age: 18 }
];

const user = users.find(u => u.age === 18);
console.log(user.name); // 张三
```

### 2.3 findIndex

返回第一个通过测试的元素的索引：

```javascript
const arr = [1, 2, 3, 4, 5];

const index = arr.findIndex(item => item > 3);
console.log(index); // 3
```

### 2.4 some

检测是否有元素通过测试，返回布尔值：

```javascript
const arr = [1, 2, 3, 4, 5];

const hasEven = arr.some(item => item % 2 === 0);
console.log(hasEven); // true
```

### 2.5 every

检测是否所有元素都通过测试：

```javascript
const arr = [2, 4, 6, 8];

const allEven = arr.every(item => item % 2 === 0);
console.log(allEven); // true
```

---

## 三、转换类

### 3.1 reduce

将数组归约为单个值：

```javascript
const arr = [1, 2, 3, 4, 5];

// 求和
const sum = arr.reduce((acc, cur) => acc + cur, 0);
console.log(sum); // 15

// 统计出现次数
const count = arr.reduce((acc, cur) => {
  acc[cur] = (acc[cur] || 0) + 1;
  return acc;
}, {});
console.log(count); // {1:1, 2:1, 3:1, 4:1, 5:1}

// 二维数组转一维
const nested = [[1, 2], [3, 4], [5]];
const flat = nested.reduce((acc, cur) => [...acc, ...cur], []);
console.log(flat); // [1, 2, 3, 4, 5]
```

### 3.2 flat

将多维数组展平：

```javascript
const arr = [1, [2, [3, [4]]]];

// 指定深度
console.log(arr.flat(2)); // [1, 2, 3, [4]]

// 全部展平
console.log(arr.flat(Infinity)); // [1, 2, 3, 4]
```

### 3.3 flatMap

先 map 再 flat：

```javascript
const arr = [1, 2, 3];

const result = arr.flatMap(x => [x * 2]);
console.log(result); // [2, 4, 6]

// 等价于
const result2 = arr.map(x => [x * 2]).flat();
```

---

## 四、排序与搜索

### 4.1 sort

对数组排序（默认按Unicode编码）：

```javascript
const arr = [3, 1, 4, 1, 5];

// 默认排序（可能出错）
console.log(arr.sort()); // [1, 1, 3, 4, 5]

// 数字排序必须传入比较函数
arr.sort((a, b) => a - b);  // 升序
arr.sort((a, b) => b - a);  // 降序

// 对象数组排序
const users = [
  { name: '张三', age: 20 },
  { name: '李四', age: 18 }
];
users.sort((a, b) => a.age - b.age);
```

### 4.2 reverse

反转数组：

```javascript
const arr = [1, 2, 3];
console.log(arr.reverse()); // [3, 2, 1]
```

### 4.3 indexOf / lastIndexOf

查找元素位置：

```javascript
const arr = [1, 2, 3, 2, 1];

console.log(arr.indexOf(2));      // 1
console.log(arr.lastIndexOf(2));  // 3
```

### 4.4 includes

检测是否包含某个值：

```javascript
const arr = [1, 2, 3];

console.log(arr.includes(2));  // true
console.log(arr.includes(4));  // false
```

---

## 五、增删改类

### 5.1 push / pop

末尾添加/删除：

```javascript
const arr = [1, 2, 3];

arr.push(4);      // 返回新长度 4
console.log(arr); // [1, 2, 3, 4]

arr.pop();        // 返回被删除的元素 4
console.log(arr); // [1, 2, 3]
```

### 5.2 unshift / shift

开头添加/删除：

```javascript
const arr = [1, 2, 3];

arr.unshift(0);   // 返回新长度 4
console.log(arr);  // [0, 1, 2, 3]

arr.shift();      // 返回被删除的元素 0
console.log(arr); // [1, 2, 3]
```

### 5.3 splice

万能的增删改：

```javascript
const arr = [1, 2, 3, 4, 5];

// 删除：起始位置，删除数量
arr.splice(1, 2);  // 删除 2,3，返回 [2,3]
console.log(arr);   // [1, 4, 5]

// 插入：起始位置，0，要插入的元素
arr.splice(1, 0, 2, 3);  // 在位置1插入 2,3
console.log(arr);   // [1, 2, 3, 4, 5]

// 替换：起始位置，删除数量，要插入的元素
arr.splice(1, 2, 'a', 'b');
console.log(arr);   // [1, 'a', 'b', 4, 5]
```

### 5.4 slice

截取数组（不修改原数组）：

```javascript
const arr = [1, 2, 3, 4, 5];

console.log(arr.slice(1, 3));   // [2, 3]
console.log(arr.slice(-2));      // [4, 5]
console.log(arr.slice());        // 拷贝数组
```

---

## 六、组合类

### 6.1 concat

合并数组：

```javascript
const arr1 = [1, 2];
const arr2 = [3, 4];
const arr3 = [5];

console.log(arr1.concat(arr2, arr3)); // [1, 2, 3, 4, 5]
```

### 6.2 join

数组转字符串：

```javascript
const arr = ['a', 'b', 'c'];

console.log(arr.join());      // 'a,b,c'
console.log(arr.join(''));    // 'abc'
console.log(arr.join('-'));   // 'a-b-c'
```

### 6.3 at

ES2022 新增，支持负索引：

```javascript
const arr = [1, 2, 3];

console.log(arr.at(0));   // 1
console.log(arr.at(-1));  // 3
console.log(arr.at(-2));  // 2
```

---

## 七、实战用法

### 7.1 去重

```javascript
// 方法1: Set
const unique = [...new Set(arr)];

// 方法2: filter
const unique = arr.filter((item, index) => arr.indexOf(item) === index);
```

### 7.2 随机打乱

```javascript
const shuffle = arr => arr.sort(() => Math.random() - 0.5);
```

### 7.3 分类统计

```javascript
const fruits = ['apple', 'banana', 'orange', 'apple', 'banana'];

const count = fruits.reduce((acc, cur) => {
  acc[cur] = (acc[cur] || 0) + 1;
  return acc;
}, {});
// { apple: 2, banana: 2, orange: 1 }
```

---

## 八、方法对比

| 方法 | 返回值 | 改变原数组 |
|------|--------|-----------|
| forEach | undefined | ❌ |
| map | 新数组 | ❌ |
| filter | 新数组 | ❌ |
| reduce | 任意值 | ❌ |
| find | 元素或undefined | ❌ |
| some | 布尔值 | ❌ |
| every | 布尔值 | ❌ |
| push | 新长度 | ✅ |
| pop | 删除的元素 | ✅ |
| sort | 排序后的数组 | ✅ |
| splice | 被删除的元素 | ✅ |

---

掌握这些方法，日常开发就够用了。建议动手实践一下，有问题欢迎留言！
