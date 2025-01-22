---
title: CSS3 学习笔记
date: 2024-12-30 10:05:37
permalink: /pages/456ff6/
sidebar: auto
categories: 
  - 随笔
tags: 
  - 
author: 
  name: lumengde
  link: https://github.com/lumengde123
---

# CSS3的现状

- 新增的CSS3特性有兼容性问题，ie9+才支持
- 移动端支持优于PC端
- 不断改进中
- 应用相对广泛
- 现阶段主要学习：新增选择器和盒子模型以及其他特性

# 新增选择器

CSS3给我们新增了三个强大的选择器，可以更快更便捷的选择目标元素

- 属性选择器
- 结构伪类选择器
- 伪元素选择器

## 属性选择器

```css
<style>
    /* 必须是input 但是同时具有 value这个属性 选择这个元素  [] */
    input[value] {
        color:pink;
    }
    /* 只选择 type =text 文本框的input 选取出来 */
    input[type=text] {
        color: pink;
    }
    /* 选择首先是div 然后 具有class属性 并且属性值 必须是 icon开头的这些元素 */
    div[class^=icon] {
        color: red;
   }
    section[class$=data] {
        color: blue;
    }
    div.icon1 {
        color: skyblue;
    }
    /* 类选择器和属性选择器 伪类选择器 权重都是 10 */
</style>
```



| 选择符        | 简介                                              |
| ------------- | ------------------------------------------------- |
| E[att]        | 选择具有 att 属性的 E 元素                        |
| E[att="val"]  | 选择具有 att 属性 且属性值为 val 的 E 元素        |
| E[att^="val"] | 匹配具有 att 属性 且 值以 val 开头的 E 元素       |
| E[att$="val"] | 匹配具有 att 属性的元素 且 值以 val 结尾的 E 元素 |
| E[att*="val"] | 匹配具有 att 属性 且 值中含有 val 的 E 元素       |

- **类选择器**、**属性选择器**、**伪类选择器**、权重都是 **10**

| 选择器                           | 选择器权重 |
| -------------------------------- | ---------- |
| 继承 / *                         | 0, 0, 0, 0 |
| 标签选择器                       | 0, 0, 0, 1 |
| 类选择器，属性选择器，伪类选择器 | 0, 0, 1, 0 |
| ID选择器                         | 0, 1, 0, 0 |
| 行内样式 style=""                | 1, 0, 0, 0 |
| !important 重要的                | ∞          |

**注意！** **继承的权重是0**。如果给自己写了样式，那么将会覆盖继承的样式

## 结构伪类选择器

主要根据文档结构来选择元素，常用于根据父级选择里面的子元素

| 选择符           | 简介                         |
| ---------------- | ---------------------------- |
| E:first-child    | 匹配父元素中的第一个子元素 E |
| E:last-child     | 匹配父元素中最后一个 E 元素  |
| E:nth-child(n)   | 匹配父元素中的第 n 个子元素E |
| E:first-of-type  | 指定类型 E 的第一个          |
| E:last-of-type   | 指定类型 E 的最后一个        |
| E:nth-of-type(n) | 指定类型 E 的第 n 个         |

**nth-child(n)**：选择某个父元素的一个或者多个特定的子元素

- `n` 可以是数字、关键字和公式；
- `n` 如果是数字，则 n 从1开始
- n可以是关键字：例如even表示偶数，odd表示奇数
- n 可以是公式：常见的公式——如果n是公式，则n从0开始计算，但是第0个元素或者超出了元素的个数会被忽略

```css
<style>
    /* 1. 选择ul里面的第一个孩子 小li */
    ul li:first-child { }
    /* 2. 选择ul里面的最后一个孩子 小li */
    ul li:last-child { }
    /* 3. 选择ul里面的第2个孩子 小li */
    ul li:nth-child(2) { }
	/* 1.把所有的偶数 even的孩子选出来 */
    ul li:nth-child(even) { }
    /* 2.把所有的奇数 odd的孩子选出来 */
    ul li:nth-child(odd) { }
	/* 3.nth-child(n) 从0开始 每次加1 往后面计算  这里面必须是n 不能是其他的字母 选择了所有的孩子*/
    ol li:nth-child(n) { } 
    /* 4.nth-child(2n)母选择了所有的偶数孩子 等价于 even */
    ol li:nth-child(2n) { }
    ol li:nth-child(2n+1) { } 
	/* 从第5个开始选 */
    ol li:nth-child(n+3) { } 
	/* 前3个，包括第3个 */
    ol li:nth-child(-n+3) { }
</style>
```

**nth-of-type(n)**：选择指定类型 E 的一个或者多个特定的子元素

```css
<style>
    ul li:first-of-type {
        background-color: pink;
    }
    ul li:last-of-type {
        background-color: pink;
    }
    ul li:nth-of-type(even) {
        background-color: skyblue;
    }
    /* nth-child 会把所有的盒子都排列序号 */
    /* 执行的时候首先看  :nth-child(1) 之后回去看 前面 div */

    section div:nth-child(1) {
        background-color: red;
    }
    /* nth-of-type 会把指定元素的盒子排列序号 */
    /* 执行的时候首先看  div指定的元素  之后回去看 :nth-of-type(1) 第几个孩子 */
    section div:nth-of-type(1) {
        background-color: blue;
    }
</style>
```

```html
<!-- 区别 -->
<section>
    <p>光头强</p>
    <div>熊大</div>
    <div>熊二</div>
</section>
```

P286





















