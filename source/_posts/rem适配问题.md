---
title: rem适配问题
date: 2019-08-19 14:57:58
tags: "盒模型"
---

## 如何把 UE 图中获取像素单位值转换位 rem 单位的值

- 公式是元素宽度/UE 宽度*100,让我们举个例子,假设 UE 图尺寸是 640px,UE 图中的一个元素宽度是 100px,根据公式 100/640*100=15.625

## 一：使用 rem 来设置字体

1. 为了方便计算字体，我们来设置浏览器 10px，我们都知道浏览器默认的像素是 16px，因此我们需要对 html{font-size:62.5%;} // 10 / 16 = 62.5%;

2. 首先假如设计搞在移动端上是按照 750px 设计稿上的话，假如字体在 750px 下字体大小我们使用 rem 来写大小；那么他们的字体大小在各个独立像素下如下计算：

- 针对设备独立像素为 640px ~ 999px 的 css

```css
@media (min-width: 640px) and (max-width: 999px) {
  /* 750/640 = 1.17*/

  html {
    font-size: 53.42%;
  } /*62.5% / 1.17 */
}

@media (min-width: 400px) and (max-width: 450px) {
  /*  750 / 400 = 1.875 */

  html {
    font-size: 33.33%;
  } /* 62.5% / 1.875 */
}

@media (min-width: 360px) and (max-width: 399px) {
  /*  750 / 360 = 2.08 */

  html {
    font-size: 30%;
  } /* 62.5% / 2.08  */
}

@media (min-width: 320px) and (max-width: 359px) {
  /*  750/320 = 2.34 */

  html {
    font-size: 26.7%;
  } /* 62.5 / 2.34 */
}
```

## 二： 针对宽度，高度，background-size, margin 及 padding 的计算方法；

1. 假如在 750px 下的宽度是 132px；高度是 132px；background-size:132px 132px; margin:20px;Padding:20px;
   针对设备独立像素为 640px ~ 999px 的 css

```css
@media (min-width: 640px) and (max-width: 999px) {
  /* 750/640 = 1.17*/

  html {
    font-size: 53.42%;
  } /*62.5% / 1.17 */

  // 下面的属性都是 本身的像素 / 1.17 得来的

  width: 112.82px; // 132 / 1.17

  height: 112.82px; // 132 / 1.17

  background-size: 112.82px 112.82px; // 132 / 1.17

  margin: 17.09px; // 20 / 1.17

  padding: 17.09px; // 20 / 1.17
}
```
