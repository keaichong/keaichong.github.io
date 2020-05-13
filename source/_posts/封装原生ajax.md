---
title: 封装原生ajax
date: 2019-02-03 23:22:34
tags: ajax
---

## 什么是 ajax

1. Ajax 即“Asynchronous Javascript And XML”（异步 JavaScript 和 XML），是指一种创建交互式网页应用的网页开发技术。
2. Ajax = 异步 JavaScript 和 XML（标准通用标记语言的子集）。
3. Ajax 是一种用于创建快速动态网页的技术。
4. Ajax 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。通过在后台与服务器进行少量数据交换，Ajax 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。传统的网页（不使用 Ajax）如果需要更新内容，必须重载整个网页页面。
<!-- more -->

## ajax 基本步骤

```js
//浏览器提供一个XMLHttpRquest类型对象,代理浏览器发送请求 并获取一部分数据
var xhr = new XMLHttpRequest();
//请求行 请求方式和路径
xhr.open("get", "/big-data");
//post请求还要设置请求头中content-type
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
//发送请求 请求体 post有请求体 get没有请求体
xhr.send(null);
//注册事件
xhr.onreadystatechange = function() {
  if (this.readyState === 4) {
    //响应体下载完成 打印响应体内容
    console.log(this.responseText);
    console.log(this.status);
    console.log(this.statusText);
  }
};
```

## 简单封装 ajax

```js
// 请求方式  路径  请求数据(请求体&查询字符串 对象形式)  回调==用于获取服务器返回的响应体
function ajax(method, path, data) {
  // 把用户传入请求方式转为大写
  method = method.toUpperCase();
  //用空数组接收 构造post请求体&get查询字符串
  var arr = [];
  for (var key in data) {
    //属性=值&属性=值
    arr.push(key + "=" + data[key]);
  }
  //通过数组join方法用&符号连接为字符串 例:?id=2&name=zs
  str = arr.join("&");
  //判断请求方式
  //get 在路径后拼接上查询字符串
  if (method === "GET") {
    path = path + (path.includes("?") ? "&" : "?") + str;
  }
  //建立xhr对象
  var xhr = new XMLHttpRequest();
  //创建http请求
  xhr.open(method, path, true);
  //判断 是否发送请求体
  if (method === "POST") {
    //post 要设置请求头中content-type请求体内容类型
    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
    //发送请求体
    xhr.send(str);
  } else {
    //get
    xhr.send(null);
  }
  //注册事件 接收服务器返回结果
  xhr.onreadystatechange = function() {
    if (this.readyState !== 4) return;
    // try 尝试着执行代码 catch 如果执行出错，会被catch 捕获到错误
    try {
      //解析返回数据 响应体 把json格式字符串转为 对象
      //接受的不是json格式字符串再json.parse转换时候  会报错 catch捕获错误 继续执行
      // JSON格式，属性和字符串类型，必须使用双引号
      // res.send('{"name": "zs", "age": 18 }');
      var obj = JSON.parse(this.responseText);
      //第四个参数 调用回调函数
      // 作用: 把obj 传给第四个参数(回调函数)接收 不然无法接受响应体
      callback(obj);
    } catch (err) {
      callback(err);
    }
  };
}
```

## 调用封装的 ajax 方法

```js
ajax(
  "post",
  "/add1",
  {
    name: "lisi",
    age: 18
  },
  function(data) {
    //data 是传过来的obj this.responseText
    console.log(data);
    console.log("我接下来要做的事");
  }
);
```
