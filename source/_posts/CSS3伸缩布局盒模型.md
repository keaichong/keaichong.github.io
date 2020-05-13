---
title: CSS3伸缩布局盒模型
date: 2019-02-02 17:03:21
tags: "盒模型"
---

### 伸缩布局基本概念

> CSS3 引入的布局模式 Flexbox 布局，主要思想是让容器有能力让其子项目能够改变其宽度，高度，以最佳方式填充可用空间。Flex 容器使用 Flex 项目可以自动放大与收缩，用来填补可用的空闲空间。更重要的是，Flexbox 布局方向不可预知，不像常规的布局(块级从上到下，内联从左到右)，而那些常规的适合页面布局，但对于支持大型或者复杂的应
> 布局解决方案 没有具体数字,通过一系列属性控制

### 伸缩盒模型术语

> 伸缩盒子中有两条轴 ->主轴和侧轴
> **主轴**: 默认水平从左往右显示

```css
/* 设置主轴方向 */
flex-direction:row | column
/* 设置元素在主轴方向对齐方式 */
justify-content: flex-start;  主轴开始位置对齐
justify-content: flex-end;    主轴结束位置对齐
justify-content: flex-center;    主轴中间显示
justify-content: space-between;    两端对齐中间自适应
justify-content: space-around;  环绕对齐
```

<!-- more -->

**侧轴** :始终垂直与主轴

```css
/* 设置元素在侧轴方向对齐方式 */
align-items:flex-start | flex-end | center | baseline | stretch

flex-start:伸缩项目在侧轴起点边的外边距紧靠住该行在侧轴起始的边。
flex-end:伸缩项目在侧轴终点边的外边距靠住该行在侧轴终点的边。
center:伸缩项目的外边距盒在该行的侧轴上居中放置。
baseline:如果伸缩项目的行内轴与侧轴为同一条，则该值和flex-start等效。其它情况下，该值将参与基线对齐。所有参与该对齐方式的伸缩项目将按下列方式排列：首先将这些伸缩项目的基线进行对齐，随后其中基线至侧轴起点边的外边距距离最长的那个项目将紧靠住该行在侧轴起点的边。
stretch:拉伸(和父盒子宽高一样)
### Flex容器属性
```

> 要改变元素的模式为伸缩容器,需要使用 display 属性.

```css
display: flex | inline-flex;
```

> inline-flex 内联伸缩容器

### flex-wrap 换行

> 默认情况下，Flex 项目都尽可能在一行显示，会导致子元素原来的宽高失效.所以你可以根据 flex-wrap 的属性值来改变，让 Flex 项目多行显示。

```css
flex-wrap: warp | nowarp 默认nowarp;
```

### 元素换行后对齐方式

```css
align-content: flex-start | flex-end | center |space-between |space-around|
  strech;
```

### 设置子元素属性

伸缩比 flex:1

### 设置元素自身对齐方式

align-self: center|auto |flex-start| flex-end

### 设置子元素排列顺序

order:1,2,3 默认 0 数字越小越靠前显示

## 视口单位

根据 CSS3 规范，视口单位主要包括以下 4 个：

      1.vw：1vw等于视口宽度的1%。

      2.vh：1vh等于视口高度的1%。

      3.vmin：选取vw和vh中最小的那个。

      4.vmax：选取vw和vh中最大的那个。

vh and vw：相对于视口的高度和宽度，而不是父元素的（CSS 百分比是相对于包含它的最近的父元素的高度和宽度）。1vh 等于 1/100 的视口高度，1vw 等于 1/100 的视口宽度。

## css3 calc
https://www.cnblogs.com/avon/p/5908393.html
- calc() 函数用于动态计算长度值。

- 需要注意的是，运算符前后都需要保留一个空格，例如：width: calc(100% - 10px)；

如果你的元素宽度是 100%时，只要你在元素中添加了 border,padding,margin 任何一值，都将会把元素盒子撑破（标准模式下，除 IE 怪异模式）。
为了解决撑破容器的问题，以前我们只能去计算 div.box 的宽度，用容器宽度减去 padding 和 border 的值，但有时候，我们苦于不知道元素的总宽度，比如说是自适应的布局，只知道一个百分值，但其他的值又是 px 之类的值，这就是难点，死卡住了。随着 CSS3 的出现，其中利用 box-sizing 来改变元素的盒模型类型实使实现效果，但今天我们学习的 calc()方法更是方便。
知道总宽度是 100%，在这个基础上减去 boder 的宽度（5px _ 2 = 10px）,在减去 padding 的宽度（10px _ 2 = 20px），即"100% - (10px + 5px) \* 2 = 30px" ，最终得到的值就是 div.box 的 width 值：
