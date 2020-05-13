---
title: localStoragr和cookie区别用法
date: 2019-02-14 17:43:23
tags:
---

## localStorage

> localStorage 生命周期是永久，这意味着除非用户显示在浏览器提供的 UI 上清除 localStorage 信息，否则这些信息将永远存在。存放数据大小为一般为 5MB,而且它仅在客户端（即浏览器）中保存，不参与和服务器的通信。

## sessionStorage

> sessionStorage 仅在当前会话下有效，关闭页面或浏览器后被清除。存放数据大小为一般为 5MB,而且它仅在客户端（即浏览器）中保存，不参与和服务器的通信。源生接口可以接受，亦可再次封装来对 Object 和 Array 有更好的支持。

- localStorage 和 sessionStorage 使用时使用相同的 API：
- 写入和读取都有三种写法
  <!-- more -->

```js
var storage = window.localStorage;
//写入a字段
storage["a"] = 1;
//写入b字段
storage.a = 1;
//写入c字段
storage.setItem("c", 3);
```
{% asset_img localStorage.png  %}
```js
//官方推荐写法
 localStorage.setItem("key","value");//以“key”为名称存储一个值“value”

localStorage.getItem("key");//获取名称为“key”的值

localStorage.removeItem("key");//删除名称为“key”的信息。

localStorage.clear();​//清空localStorage中所有信息
```

京东官网顶部的广告关闭，效果为第一次进入官网会出现广告，然后点击关闭，刷新网页不会再显示广告，但是当清除 localStorage 存入的数据，刷新网页会再显示广告。
苏宁官网顶部广告数据保存在 cookie 中,当清除 cookie 中的数据时候,刷新网页也会再次显示广告

京东广告相关 js 写法

```js
//localStorage方法
<script src="../js/jquery.min.js" />;
function haxi() {
  //判断localStorage里有没有isClose
  if (localStorage.getItem("isClose")) {
    $(".header").hide();
  } else {
    $(".header").show();
  }
  //点击关闭隐藏图片存取数据
  $(".close").click(function() {
    $(".header").fadeOut(1000);

    localStorage.setItem("isClose", "1");
  });
}
haxi();
```

### 作用域不同

不同浏览器无法共享 localStorage 或 sessionStorage 中的信息。相同浏览器的不同页面间可以共享相同的 localStorage（页面属于相同域名和端口），但是不同页面或标签页间无法共享 sessionStorage 的信息。这里需要注意的是，页面及标 签页仅指顶级窗口，如果一个标签页包含多个 iframe 标签且他们属于同源页面，那么他们之间是可以共享 sessionStorage 的。

## Cookie

生命期为只在设置的 cookie 过期时间之前一直有效，即使窗口或浏览器关闭。 存放数据大小为 4K 左右 。有个数限制（各浏览器不同），一般不能超过 20 个。与服务器端通信：每次都会携带在 HTTP 头中，如果使用 cookie 保存过多数据会带来性能问题。但 Cookie 需要程序员自己封装，源生的 Cookie 接口不友好

### cookie 的优点：具有极高的扩展性和可用性 
1.通过良好的编程，控制保存在 cookie 中的 session 对象的大小。 
2.通过加密和安全传输技术，减少 cookie 被破解的可能性。 
3.只有在 cookie 中存放不敏感的数据，即使被盗取也不会有很大的损失。 
4.控制 cookie 的生命期，使之不会永远有效。这样的话偷盗者很可能拿到的就 是一个过期的 cookie。

### cookie 的缺点：
1.cookie 的长度和数量的限制。每个 domain 最多只有 20 条 cookie，每个 cookie 长度不能超过 4KB。则会被截掉。 
2.安全性问题。如果 cookie 被人拦掉了，那个人就可获取到所有 session 信息。加密的话也不起什么作用。
3.有些状态不可能保存在客户端。例如，为了防止重复提表单，我们需要在服务端保存一个计数器。若吧计数器保在客户端，则起不到什么作用。
