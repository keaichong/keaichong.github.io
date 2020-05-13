---
title: 什么时候用module.export?什么时候用exports？
date: 2019-02-26 23:49:51
tags: js
---

## 创建/引用 module

假设这是 rocker.js 文件

```js
exports.name = function() {
  console.log("my name is cp");
};
```

在另一个文件中引用 rocker.js

```js
var rocker = require("./rocker.js");
rocker.name(); // my name is cp
```

<!-- more -->

**先来看一个例子**

```js
var a = { name: 1 };
var b = a;

console.log(a); // { name: 1 }
console.log(b); // { name: 1 }

b.name = 2;
console.log(a); // { name: 2 }
console.log(b); // { name: 2 }

var b = { name: 3 };
console.log(a); // { name: 2 }
console.log(b); // { name: 3 }
```

> 分析

1. 一开始,a 是一个对象，b 是对 a 的引用,即 a 和 b 指向同一块内存，所以前两个输出一样。
2. 然后对 b 做修改,即 a 和 b 指向同一块内存地址的内容发生了改变,所以 a 和 b 的输出是一样的。
3. 接着 b 被重新赋值时，这时候 b 指向了一块新的内存,a 还是指向原来的内存，所以最后两个输出不一样。

## module.exports 和 exports 到底是什么？

> 每一个 node.js 执行文件，都自动创建一个 module 对象和 exports 对象，同时，module 对象会创建一个叫 exports 的属性，初始化的值是 {}。实际上， exports 和 module.exports 指向同一块内存，可以理解为 exports 只是 module.exports 的引用，即：exports = module.exports = {};
> 其实，Module.exports 才是真正的接口，exports 只不过是它的一个辅助工具。最终返回给调用的是 Module.exports 而不是 exports。所以不要直接给 exports 赋值,可以在赋值后使用 module.exports = exports 重新将 exports 和 module.exports 关联起来。也可以直接给 module.exports 赋值。
> 所有的 exports 收集到的属性和方法，都赋值给了 Module.exports。当然，这有个前提，就是 Module.exports 本身不具备任何属性和方法。如果，Module.exports 已经具备一些属性和方法，那么 exports 收集来的信息将被忽略。原因是 require 引入的对象本质上是 module.exports。这就产生了一个问题，当 module.exports 和 exports 指向的不是同一块内存时，exports 的内容就会失效。

例如

```js
module.exports = {name: '萤火虫叔叔'}；
exports = {name: '萤火虫老阿姨'}
```

> 此时 module.exports 指向了一块新的内存（该内存的内容为{name: '萤火虫叔叔'}），exports 指向了另一块新的内存（该内存的内容为{name: '萤火虫老阿姨'}）。require 得到的是{name: '萤火虫叔叔'}。

## 什么时候用 exports？什么时候用 module.exports？

- 如果你想你的模块是一个特定的类型就用 Module.exports。
- 如果你想的模块是一个典型的“实例化对象”就用 exports。
  给 module.exports 添加属性类似于给 exports 添加属性，例如：

```js
module.export.name = function() {
  console.log("my name is cp");
};
```

同样，exports 是这样的

```js
exports.name = function() {
  console.log("my name is cp");
};
```

> 推荐使用 exports 导出，除非你打算从原来的“实例化对象”改变成一个类型。

## 总结

1.  exports 是指向的 module.exports 的引用

2.  module.exports 初始值为一个空对象 {}，所以 exports 初始值也是 {}

3.  require()返回的是 module.exports 而不是 exports

4. module.exports导出的是函数,require引入的也是函数,导出对象,require引入也是对象
