---
title: router两种方式
date: 2019-03-30 21:24:00
tags: vue-router
---

## 关于 this.\$router.push、replace、go 的用法和区别

1. this.\$router.push 跳转到指定 url 路径，并想 history 栈中添加一个记录，点击后退会返回到上一个页面
2. this.\$router.replace 跳转到指定 url 路径，但是 history 栈中不会有记录，点击返回会跳转到上上个页面
3. this.\$router.go(n)向前或者向后跳转 n 个页面，n 可为正整数或负整数

## <router-link :to="...">声明式

```html
// 字符串
<router-link to="apple"> to apple</router-link>
// 对象
<router-link :to="{path:'apple'}"> to apple</router-link>
// 命名路由
<router-link :to="{name: 'applename'}"> to apple</router-link>
//直接路由带查询参数query，地址栏变成 /apple?color=red
<router-link :to="{path: 'apple', query: {color: 'red' }}">
  to apple</router-link
>
// 命名路由带查询参数query，地址栏变成/apple?color=red
<router-link :to="{name: 'applename', query: {color: 'red' }}">
  to apple</router-link
>
//直接路由带路由参数params，params 不生效，如果提供了 path，params 会被忽略
<router-link :to="{path: 'apple', params: { color: 'red' }}">
  to apple</router-link
>
// 命名路由带路由参数params，地址栏是/apple/red
<router-link :to="{name: 'applename', params: { color: 'red' }}">
  to apple</router-link
>
```

## router.push(...) 编程式方法

```js
// 字符串
router.push("apple");
// 对象
router.push({ path: "apple" });
// 命名路由
router.push({ name: "applename" });
//直接路由带查询参数query，地址栏变成 /apple?color=red
router.push({ path: "apple", query: { color: "red" } });
// 命名路由带查询参数query，地址栏变成/apple?color=red
router.push({ name: "applename", query: { color: "red" } });
//直接路由带路由参数params，params 不生效，如果提供了 path，params 会被忽略,必须使用命名路由
router.push({ path: "applename", params: { color: "red" } });
// 命名路由带路由参数params，地址栏是/apple/red
router.push({ name: "applename", params: { color: "red" } });
```

## 注意点

1. 关于带参数的路由总结如下

- 无论是直接路由“path" 还是命名路由“name”，带查询参数 query，地址栏会变成“/url?查询参数名：查询参数值“;
- 直接路由“path" 带路由参数 params params 不生效;
- 命名路由“name" 带路由参数 params 地址栏保持是“/url/路由参数值”;

2. 设置路由 map 里的 path 值：

- 带路由参数 params 时，路由 map 里的 path 应该写成: path:'/apple/:color' ;
- 带查询参数 query 时，路由 map 里的 path 应该写成: path:'/apple' ；

3. 获取参数方法：

- 在 template 中：{{$route.params.color}}
- 在 script 里： this.\$route.params.color
