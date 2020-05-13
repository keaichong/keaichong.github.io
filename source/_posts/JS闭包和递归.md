---
title: JS闭包和递归
date: 2019-02-02 23:42:32
tags: "js"
---

### 闭包 closure

> 闭包是一个子函数，子函数一定要把内部和外部关联起来。闭包满足两个条件 一,让内部和外部关联 二,内层子函数可以操作到外层函数变量
> 理解:函数作为返回值，函数作为参数传递

1. 变量保存在内存中 变量的生命周期: 变量什么时候被释放
2. 全局变量生命周期: 退出程序后才会被释放
3. 局部变量生命周期: 函数调用时候产生,本次结束后释放局部变量

### 作用域

作用域是在函数定义时决定的,从内层向外层访问
问题: 外层作用域无法操作内层作用域变量
原因: 局部作用域生命周期在调用结束后释放了,因此外层不能访问.
需求: 让外层作用域操作到内层作用域
实现: 用闭包来延长局部变量的生命周期

### 闭包中的 GC 垃圾回收机制
<!-- more -->
运行中的程序的数据是存放在内存中  
 在运行的过程中有一个叫 GC 的机制（Garbage Collection 垃圾回收机制）
GC 相当于生活中的保洁，会不定时去清理内存中的没有用的数据,也就是不在被引用的数据。

```js
function bieShu() {
  var a = 3; // 局部变量
  var guanjia = function(num) {
    // 管家
    console.log(a);
    a = a + num;
    console.log(a);
  };
  return guanjia;
}
var cyqz = bieShu();
// 若函数内部中的a不在了，10 是无法和a相加的得出结果13的
// 若a还在，10 和 a得出结果是13， 说a在bieshu这函数调用完毕后没有被释放。
// 怎么延长的？ 内部的子函数当做桥梁和外部关联→ 外部直在应用或操作函数内部的局部变量→ 所以局部变量没有当做垃圾数据释放
cyqz(10); // a = 13
cyqz(10); // a = 23
cyqz(10); // a = 23
// 如何调试： 在子函数内部设置断点→ 进入子函数内部后 → 查看右侧是否有clouser存在
```

### 闭包用途

1. 函数外部读取函数内部成员
2. 函数内成员始终存活在内存之中(延长局部变量生命周期)
3. 维护私有变量的安全(例如 取款机取钱)

```javascript
var name = "The Window";
var object = {
  name: "My Object",
  getNameFunc: function() {
    return function() {
      console.log(this.name); //The Window
    };
  }
};
var fn = object.getNameFunc();
fn();
```

```javascript
var name = "The Window";
var object = {
  name: "My Object",
  getNameFunc: function() {
    var that = this;
    return function() {
      console.log(that.name); //My Object
    };
  }
};
var fn = object.getNameFunc();
window.fn();
```

### 递归

> 程序调用自身 作用:减少代码量

### 递归的三个阶段

- 递归前进段
- 递归边界条件
- 递归返回段
  1,1,2,3,5,8..........求第 n 个数是多少 斐波那契数列 用递归实现

```js
function getFbi(n) {
  if (n == 1 || n == 2) {
    return 1;
  }
  return getFbi(n - 1) + getFbi(n - 2);
}
console.log(getFbi(6));
```
