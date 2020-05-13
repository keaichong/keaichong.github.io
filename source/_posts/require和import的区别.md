---
title: require和import的区别
date: 2019-02-10 01:16:42
tags: js
---
>node编程中最重要的思想就是模块化，import和require都是被模块化所使用。

## 遵循规范

1. require 是 AMD规范引入方式
2. import是es6的一个语法标准，如果要兼容浏览器的话必须转化成es5的语法
## 调用时间

1. require是运行时调用，所以require理论上可以运用在代码的任何地方
2. import是编译时调用，所以必须放在文件开头
## 本质

1. require是赋值过程，其实require的结果就是对象、数字、字符串、函数等，再把require的结果赋值给某个变量
2. import是解构过程，但是目前所有的引擎都还没有实现import，我们在node中使用babel支持ES6，也仅仅是将ES6转码为ES5再执行，import语法会被转码为require
<!-- more -->
## require / exports ：
1. 遵循 CommonJS/AMD，只能在运行时确定模块的依赖关系及输入/输出的变量，无法进行静态优化。用法只有以下三种简单的写法：
```js
const fs = require('fs')
exports.fs = fs
module.exports = fs
```
## import / export：
1. 遵循 ES6 规范，支持编译时静态分析，便于JS引入宏和类型检验。动态绑定。
2. 写法就比较多种多样：(导入的时候有没有大括号的区别是什么)
    1.当用export default people导出时，就用 import people 导入（不带大括号）

    2.一个文件里，有且只能有一个export default。但可以有多个export。

    3.当用export name 时，就用import { name }导入（记得带上大括号）

    4.当一个文件里，既有一个export default people, 又有多个export name 或者 export age时，导入就用 import people, { name, age } 

    5.当一个文件里出现n多个 export 导出很多模块，导入时除了一个一个导入，也可以用import * as example
```js
import fs from 'fs'
import {default as fs} from 'fs'
import * as fs from 'fs'
import {readFile} from 'fs'
import {readFile as read} from 'fs'
import fs, {readFile} from 'fs'
 
export default fs
export const fs
export function readFile
export {readFile, read}
export * from 'fs'
 ```
通过require引入基础数据类型时，属于复制该变量。
通过require引入复杂数据类型时，数据浅拷贝该对象。
出现模块之间的循环引用时，会输出已经执行的模块，而未执行的模块不输出（比较复杂）
CommonJS模块默认export的是一个对象，即使导出的是基础数据类型
