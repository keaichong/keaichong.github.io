---
title: vue-router的history坑
date: 2019-08-14 14:20:04
tags: vue-router
---

## 解决使用 vue-cli 生成项目后项目地址自动添加#号的问题

**vue 的路由在默认的 hash 模式下,url 会带有一个#,不美观,而且在微信分享,授权登录等都会有一些坑.所以 history 模式（不带#号）也会有一些应用场景.**

## 问题一：

**变为 history 模式，子路由在刷新情况下会出现样式变乱的情况，解决方法如下：**
<!-- more -->
- 直接修改 index.html 文件中的静态文件引入路径就 OK 了

1. 修改前:<link rel="stylesheet" href="./static/css/base.css">

2. 修改后:<link rel="stylesheet" href="/static/css/base.css">

## 修改原理：

1. ./ 是指用户所在的当前目录（相对路径）；

2. / 是指根目录（绝对路径，项目根目录），也就是项目根目录；

3. 对于 hash 模式，根路径是固定的，就是项目的根目录，但是 history 模式下，以 / 开头的嵌套路径会被当作根路径，所以使用“./”引入文件，就会找不到文件了，因为文件本身就是在项目根目录下的，并不在嵌套路径这个目录下。

4. 总结，无论 hash 模式还是 history 模式，可以直接使用“/”从项目根目录引入静态文件。

## 问题二:

**vue 的路由在默认的 hash 模式下,默认打包一般不会有什么问题，而 history 模式打包后回出现页面一片空白的情况,而且没有资源加载错误的报错信息.**

1. 参考文章https://www.jb51.net/article/142831.htm

2. https://blog.csdn.net/g1531997389/article/details/79154179
