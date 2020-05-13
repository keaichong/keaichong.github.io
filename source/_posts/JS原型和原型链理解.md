---
title: JS原型和原型链理解
date: 2019-02-03 01:47:36
tags: "js"
---

## 原型的作用

1. 前提：① 将来对象的空间大小，和对象的属性和方法数量有关；② 属性是不一致的，方法是一致。
2. 问题：内存的浪费
3. 原因：对象的方法是一致的，每创建一个对象，都为每一个对象分配一个属于各自的方法，方法的数量随 1. 对象的个数，方法数量越来越多。 方法 → 函数 → 数据类型 → 内存
4. 解决：把多个方法抽取成一个，让所有同类型的对象共享之。
5. 如何实现：通过原型，把方法放入到原型中，就可以被构造函数创建的对象共享。

## 对象查找属性和方法的流程

1. 会先从实例对象本身查找
2. 如果没找到,实例对象通过构造函数对象.*proto*所提供的原型地址找到原型
3. 从原型中查找要访问属性或方法
4. 如果还是没找到,则在原型对象.*proto*中查找，一直到 null，如果没有则返回 undefined

## 获取原型

> 语法:函数名.prototype

## 获取构造函数

> 语法: 原型.constructor
<!-- more -->
## 原型添加属性方法

> 语法:函数名.prototype.key = value

> 注意:数组和字符串中的 prototype 不要修改,修改后自带的方法就没有了,可以采用添加方式

```js
Array.prototype.getMax = function() {};
```

## JQuery 原型添加方法

> 语法:$.prototype.方法 = function(){}
> 简写:  $.fn.方法 = function(){}

## 构造函数

```js
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function() {
    alert(this.name);
  };
}
var person1 = new Person("Zaxlct", 28, "Software Engineer");
var person2 = new Person("Mick", 23, "Doctor");
```

上面的例子中 person1 和 person2 都是 Person 的实例。这两个实例都有一个 constructor （构造函数）属性，该属性（是一个指针）指向 Person。 即

```js
console.log(person1.constructor == Person); //true
console.log(person2.constructor == Person); //true
```

person1 和 person2 都是 构造函数 Person 的实例
实例的构造函数属性（constructor）指向构造函数。

## 原型对象

> 在 JavaScript 中，每当定义一个对象（函数也是对象）时候，对象中都会包含一些预定义的属性。其中每个函数对象都有一个 prototype 属性，这个属性指向函数的原型对象。

```js
function Person() {}
Person.prototype.name = "Zaxlct";
Person.prototype.age = 28;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function() {
  alert(this.name);
};

var person1 = new Person();
person1.sayName(); // 'Zaxlct'

var person2 = new Person();
person2.sayName(); // 'Zaxlct'

console.log(person1.sayName == person2.sayName); //true
```

## 认识原型链

```js
// 给Object的构造函数的原型添加了一个属性a
Object.prototype.a = 123;

// 【构造函数】
function Hero(name, age) {
  // 属性
  this.name = name;
  this.age = age;
}

//【获取原型】
var yx = Hero.prototype;
// 语法：对象.key = value
yx.attack = function() {
  console.log(this.name + "正在发飙....");
};
yx.type = "英雄";

// 创建一个英雄对象
var hy = new Hero("后裔", 10);
console.log(hy.type);

// 原型链
// 属性的查找规则
// ① 从对象本身中查找，若没找到
// ② 则通过__proto__提供的原型的地址，找到yx，从yx中查找，若也没找到
// ③ 在原型的中也有一个__proto__，则会通过__proto__找到原型的原型
// 这个查找的过程之所以能够执行，是因为原型链的存。
console.log(hy.a);
console.log(hy.__proto__); // Hero.prototype
console.log(hy.__proto__.__proto__); // Object.prototype
console.log(hy.__proto__.__proto__ === Object.prototype); // true
console.log(hy.__proto__.__proto__.__proto__); // null
```
