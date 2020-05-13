---
title: exportdefault和export的使用方式
date: 2019-02-12 23:21:26
tags: js
---

## node 和 ES6 中导入模块区别

node 中导入模块：var 名称 = require('模块标识符')

node 中向外暴露成员的形式：module.exports = {}

在 ES6 中，也通过规范的形式，规定了 ES6 中如何导入和导出模块

ES6 中导入模块，使用 import 模块名称 from '模块标识符'    import '表示路径'

import **_ from _** 是 ES6 中导入模块的方式

<!-- more -->

## 在 ES6 中，使用 export default 和 export 向外暴露成员

例如

```js
// test.js
export default {
    name: 'zs',
    age: 20
```

或是

```js
// test.js
var info = {
  name: "zs",
  age: 20
};
export default info;
```

在 main.js 中接收，test.js 使用 export default 向外暴露的成员

```js
import person from "./test.js";
console.log(person);
```

{% asset_img 20180826175027288.png  %}

注意：

1、export default 向外暴露的成员，可以使用任意变量来接收

2、在一个模块中，export default 只允许向外暴露一次

3、在一个模块中，可以同时使用 export default 和 export 向外暴露成员

4、使用 export 向外暴露的成员，只能使用{  }的形式来接收，这种形式，叫做【按需导出】

5、export 可以向外暴露多个成员，同时，如果某些成员，在 import 导入时，不需要，可以不在{ }中定义

6、使用 export 导出的成员，必须严格按照导出时候的名称，来使用{ }按需接收

7、使用 export 导出的成员，如果想换个变量名称接收，可以使用 as 来起别名

例如:

```js
// test.js
var info = {
  name: "zs",
  age: 20
};
export default info;

export var title = "小星星";

export var content = "哈哈哈";
```

在 main.js 中接收，test.js 使用 export default 和 export 向外暴露的成员

```js
import person, { title, content as content1 } from "./test.js";
console.log(person);
console.log(title + "=======" + content1);
```
{% asset_img 20180826175958870.png  %}
