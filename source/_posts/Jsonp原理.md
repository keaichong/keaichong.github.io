---
title: Jsonp原理
date: 2019-02-04 01:13:25
tags: Jsonp
---

## jsonp 工作原理

利用 script 标签可以跨域,让服务器端返回可以执行的 Javascript 函数,参数为要回发的数据,jsonp 只能发 get 请求

## 相关概念(同源)

同源策略是浏览器的一种安全策略，所谓同源是指域名(com/cn/localhost)，协议(http/https)，端口完全相同，只有同源的地址才可以相互通过 AJAX 的方式请求。

浏览器默认情况下，不允许发送跨域的 ajax 请求

同源或者不同源说的是两个地址之间的关系，不同源地址之间请求我们称之为跨域请求

## jsonp 前端代码

```js
// 点击按钮，发送跨域的请求，获取到结果
document.querySelector("#btn").onclick = function() {
  // 1. 创建script标签
  var script = document.createElement("script");
  // 2. 设置src
  script.src = "http://localhost:3000/query?callback=song";
  // 3. 把script添加到body
  document.body.appendChild(script);
  //执行script中的代码
  //相当于
  // <script>song(data相应数据)</\script>
};
//被调用  这种方式需要前后端配合
function song(data) {
  console.log(data); //拿到跨域请求返回的数据 自己根据需要进行后续处理
}
```

<!-- more -->

## 后端代码

```js
const express = require("express");
const bodyParser = require("body-parser");
const path = require("path");
const fs = require("fs");
const app = express();
// 设置静态资源
app.use(express.static(path.join(__dirname, "public")));
let user = require("./db");
// 设置一个路由，返回js代码
// jsonp 的接口
app.get("/query", (req, res) => {
  //设置请求头
  res.setHeader("Content-Type", "application/javascript");
  // 输出的样式  fn({....});
  // 接收查询字符串中的callback
  let cb = req.query.callback;
  let jsonStr = JSON.stringify(user);
  // jsonString  --->  [{},{}];

  //返回一个调用函数名 把查询字符串的值用模板字符串设为返回的函数名,这样前端就可以通过调用函数拿到script标签返回的数据 cb是函数名song  jsonstr是实参
  let javascriptString = `${cb}(${jsonStr});`;
  //发送了一个调用方式给前端
  res.send(javascriptString);
});

app.listen(3000, () => {
  console.log("开始监听：3000");
});
```
